## redux是什么
1. redux是一个专门用于**状态管理**的js库（不是react插件库）
2. 可以在react、angular、vue等项目中运用，一般是和react配合使用
3. 作用：集中管理react中多个组件共享的状态，与vue中的vuex仓库差不多

## 什么情况下需要使用redux
1. 某个组件的状态，需要让其他组件随时可以拿到（共享）
2. 一个组件需要改变另一个组件的状态（通讯）
3. 总体原则：能不用就不用，一般用于比较复杂的业务逻辑

## redux工作流程图
![[Pasted image 20220706180015.png]]

### 三个核心概念
#### 7.2.1. action
1.  动作的对象
2.  包含2个属性
    -   type：标识属性, 值为字符串, 唯一, 必要属性
    -   data：数据属性, 值类型任意, 可选属性
3.  例子：{ type: 'ADD_STUDENT',data:{name: 'tom',age:18} }

#### 7.2.2. reducer
1.  用于初始化状态、加工状态。
2.  加工时，根据旧的state和action， 产生新的state的**纯函数。**

#### 7.2.3. store
1.  将state、action、reducer联系在一起的对象
2.  如何得到此对象?

```jsx
import {createStore} from 'redux'
import reducer from './reducers'
const store = createStore(reducer)
```

## Redux简单使用
1. redux中state每次更新后需要重新渲染render，我们有两种方式实现：
```jsx
//index.js
ReactDOM.render(<App/>,document.getElementById('root'))
store.subscribe(()=>{
    ReactDOM.render(<App/>,document.getElementById('root'))
})
```

```jsx
//组件中
componentDidMount(){
    //检测redux中状态的变化，只要变化，就调用render
    store.subscribe(()=>{
        this.setState({})
    })
}
```

2. 创建store
```js
//引入createStore，专门用于创建redux中最为核心的store对象
import {createStore} from 'redux'
//引入为Count组件服务的reducer
import countReducer from './count_reducer'
//暴露store
export default createStore(countReducer)
```

3. 创建reducer
```js
/*
    1.该文件是用于创建一个为Count组件服务的reducer，reducer的本质就是一个函数
    2.reducer函数会接到两个参数，分别为：之前的状态(preState)，动作对象(action)
*/

const initState = 0 //初始化状态
export default function countReducer(preState=initState,action){
    // console.log(preState);
    //从action对象中获取：type、data
    const {type,data} = action
    //根据type决定如何加工数据
    switch (type) {
        case 'increment': //如果是加
            return preState + data
        case 'decrement': //若果是减
            return preState - data
        default:
            return preState
    }
}
```

4. dispatch到store（**dispatch(type,data)**）
```jsx
//加法
increment = ()=>{
    const {value} = this.selectNumber
    store.dispatch({type:'increment',data:value*1})
}
//减法
decrement = ()=>{
    const {value} = this.selectNumber
    store.dispatch({type:'decrement',data:value*1})
}
```


## Redux完全版
r完全版主要是添加了action，他主要的作用是帮助用户提交dispatch的具体内容：
**组件中**
```jsx
    //加法
    increment = ()=>{
        const {value} = this.selectNumber
        store.dispatch(createIncrementAction(value*1))
    }
    //减法
    decrement = ()=>{
        const {value} = this.selectNumber
        store.dispatch(createDecrementAction(value*1))
    }
```

**action**
```jsx
import {INCREMENT,DECREMENT} from './constant'
export const createIncrementAction = data => ({type:INCREMENT,data})
export const createDecrementAction = data => ({type:DECREMENT,data})
```

**命名switch变量的集中管理**
```js
/*
    该模块是用于定义action对象中type类型的常量值，目的只有一个：便于管理的同时防止程序员单词写错
*/
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
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

## 异步action
**action**
```js
//异步action，就是指action的值为函数,异步action中一般都会调用同步action，异步action不是必须要用的。
export const createIncrementAsyncAction = (data,time) => {
    return (dispatch)=>{
        setTimeout(()=>{
            dispatch(createIncrementAction(data))
        },time)
    }
}
```
**store**(引入redux-thunk)
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

