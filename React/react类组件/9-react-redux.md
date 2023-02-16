## react-redux
1.所有的UI组件都应该包裹-个容器组件他们是父子关系。
2.容器组件是真正和redux打交道的，里面可以随意的使用redux的api。
3.UI组件中不能使用任何redux的api。
4.容器组件会传给Ul组件: (1).redux中 所保存的状态。(2).用于 操作状态的方法
5.备注:容器给UI传递:状态、操作状态的方法，均通过props传递。
![[react-redux模型图.png]]

从上图来看，我们可以发现，原本精简版的redux是由组件直接与redux操作的，现在react官方出的react-redux的原理图多了一个容器组件（它的作用就是将原本在组件中请求派发action的所有内容迁移到其中（易于管理）），我们的react-redux就与容器组件进行有效`交流`，具体的实现方式如下所示：
## React-redux的具体实现
1. 老规矩，redux需要根据变化的数据实时渲染render，所以我们将APP（整个大组件）包裹
**入口文件index.js**
```js

ReactDOM.render(<App/>,document.getElementById('root'))
//监测redux中状态的改变，如redux的状态发生了改变，那么重新渲染App组件
store.subscribe(()=>{
    ReactDOM.render(<App/>,document.getElementById('root'))
})
```

2. 创建组件的容器（**我们可以将UI组件放入component中，容器放入container中**）大商股份方式

		在容器中，我们认为是连接UI组件和redux的关键点，我们在此引入UI组件和redux，并实现dispatch的派发工作，（**派发的内容就是action中指定的同步或异步函数**）
```js
//引入Count的UI组件
import CountUI from '../../components/Count'
//引入action
import {
    createIncrementAction,
    createDecrementAction,
    createIncrementAsyncAction
} from '../../redux/count_action'
//引入connect用于连接UI组件与redux
import {connect} from 'react-redux'
```

然后，我们使用**react-redux**中的**connect**连接UI组件与redux
```js
/*
    1.mapStateToProps函数返回的是一个对象；
    2.返回的对象中的key就作为传递给UI组件props的key,value就作为传递给UI组件props的value
    3.mapStateToProps用于传递状态
*/
function mapStateToProps(state){
    return {count:state}
}
/*
    1.mapDispatchToProps函数返回的是一个对象；
    2.返回的对象中的key就作为传递给UI组件props的key,value就作为传递给UI组件props的value
    3.mapDispatchToProps用于传递操作状态的方法
*/
function mapDispatchToProps(dispatch){
    return {
        jia:number => dispatch(<createIncreme></createIncreme>ntAction(number)),
        jian:number => dispatch(createDecrementAction(number)),
        jiaAsync:(number,time) => dispatch(createIncrementAsyncAction(number,time)),
    }
}
//使用connect()()创建并暴露一个Count的容器组件
export default connect(mapStateToProps,mapDispatchToProps)(CountUI)
```
3. 将store通过props传给UI组件
```js
            <div>
                {/* 给容器组件传递store */}
                <Count store={store} />
            </div>
```
4. 创建action，reducer等redux相关文件
**store.js**
```js
//引入createStore，专门用于创建redux中最为核心的store对象
import {createStore,applyMiddleware} from 'redux'
//引入为Count组件服务的reducer
import countReducer from './count_reducer'
//引入redux-thunk，用于支持异步action
import thunk from 'redux-thunk'
//暴露store
export default createStore(countReducer,applyMiddleware(thunk))
```
**action**
```js
import {INCREMENT,DECREMENT} from './constant'
//同步action，就是指action的值为Object类型的一般对象
export const createIncrementAction = data => ({type:INCREMENT,data})
export const createDecrementAction = data => ({type:DECREMENT,data})
//异步action，就是指action的值为函数,异步action中一般都会调用同步action，异步action不是必须要用的。
export const createIncrementAsyncAction = (data,time) => {
    return (dispatch)=>{
        setTimeout(()=>{
            dispatch(createIncrementAction(data))
        },time)
    }
}
```
**reducer**
```js
import {INCREMENT,DECREMENT} from './constant'
const initState = 0 //初始化状态
export default function countReducer(preState=initState,action){
    // console.log(preState);
    //从action对象中获取：type、data
    const {type,data} = action
    //根据type决定如何加工数据
    switch (type) {
        case INCREMENT: //如果是加
            return preState + data
        case DECREMENT: //若果是减
            return preState - data
        default:
            return preState
    }
}
```
**contains**(用于存放统一管理的变量或函数名)
```js
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
```

**最后，我们通过this.props.XX来获取redux中经过数据处理后的数据**
我们如何更加清楚的理解redux呢？我们可以借助vue中vuex的相关性更好的理解redux的流程，以及文件结构：
```js
/*首先在容器中，我们看可以将其看做是一个仓库，用于存储数据结果和派发任务的地方，
在UI组件中，如果我们需要通过redux将数据修改，并取得更改后的值（亦或者是为其他组件共
享该数据，并需要修改）的时候，我们就以
this.props.关键字(参数1，参数2，等等)提交给容器

在容器中，我们使用connect(mapStateToProps,mapDispatchToProps)(CountUI)暴露
该容器，connect（）（UI）,其中前方的两个参数分别是

mapStateToProps函数返回的是一个对象，返回的对象中的key就作为传递给UI组件props的
key,value就作为传递给UI组件props的value，也就是说，该函数返回的对象中的value就是我们要修改的数据的最新值

mapDispatchToProps函数返回的是一个对象，用于传递操作状态的方法，就像vuex中去派发任务到action一样，该函数也是通过dispatch去调用action中的对象方法，并通过reducer
实现具体数据的修改

当action收到由容器dispatch来的数据的时候，会将其整理为{type(方法),data}传给reducer

reducer根据收到的不同的type方法，来实现不同的数据修改，最后暴露在store（在容器中通过props传给了UI组件）中，我们就能在UI组件中通过props获取数据
*/
```

当我们使用了react-redux之后，我们就不需要自己去监听重新渲染render了，react在connect底层中已经将其实现了。

## react-redux的优化
1. 将容器和UI组件整合为一个文件
```js
class Count extends Component{...}


export default connect(
    state => ({count:state}),
    {
        jia:createIncrementAction,
    }
)(Count)
```

2. 不需要自己传递store，只需要给APP外壳包裹一个`<Provider store={store}>`即可。

3. 不需要自己检测redux中的状态，容器组件会自己完成这个工作