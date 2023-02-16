### SPA
1. 单页面应用（single page application）
2. 整个应用只有一个完整的页面
3. 点击页面中跳转链接不会**刷新**页面，只会做页面的**局部更新**
4. 数据都需要通过ajax请求获取，并在前端异步展示。

### history
history：浏览器中以栈结构为基础的API：包括：
push，replace，goBack，goForward几个操作
push为入栈，replace为替换。

HashHistory：createHashHistory（带锚点‘#’）

### react-router-dom
安装react中web路由的插件库
```shell
npm i react-router-dom
```

内置组件：
```js
<BrowserRouter>
<HashRouter>
<Route>
<Redirect>
<Link>
<NavLink>
<Switch>
```

#### React路由的基本使用
在index.js中，我们用BrowserRouter将APP包裹，就能实现路由的编写和路由跳转由同一个BrowserRouter'监听'。
```js
//引入react核心库
import React from 'react'
//引入ReactDOM
import ReactDOM from 'react-dom'
import {BrowserRouter} from 'react-router-dom'
//引入App
import App from './App'
ReactDOM.render(
    <BrowserRouter>
        <App/>
    </BrowserRouter>,
    document.getElementById('root')
)
```

路由的使用方式如下所示：（在引入两个路由组件后）
![[Pasted image 20220705155623.png]]

```js
import React, { Component } from 'react'

import {Link,Route} from 'react-router-dom'

import Home from './components/Home'

import About from './components/About'

  

export default class App extends Component {
    render() {
        return (
            <div>
                <div className="row">
                    <div className="col-xs-offset-2 col-xs-8">
                        <div className="page-header"><h2>React Router Demo</h2></div>
                    </div>
                </div>
                <div className="row">
                    <div className="col-xs-2 col-xs-offset-2">
                        <div className="list-group">
                            {/* 原生html中，靠<a>跳转不同的页面 */}
                            {/* <a className="list-group-item" href="./about.html">About</a>
                            <a className="list-group-item active" href="./home.html">Home</a> */}
                            {/* 在React中靠路由链接实现切换组件--编写路由链接 */}
                            <Link className="list-group-item" to="/about">About</Link>
                            <Link className="list-group-item" to="/home">Home</Link>
                        </div>
                    </div>
                    <div className="col-xs-6">
                        <div className="panel">
                            <div className="panel-body">
                                {/* 注册路由 */}
                                <Route path="/about" component={About}/>
                                <Route path="/home" component={Home}/>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        )
    }
}
```

**HashRouter同样如此，多了#，#后面的信息不被作为资源发送给服务器**


一般组件和路由组件的区别主要是：
1. 路由组件不会手动写标签`<Header/>`
2. 路由组件初始在props中可以接收到参数：
![[Pasted image 20220705163004.png]]

**NavLink的使用：**
```js
<NavLink activeClassName="类名" ></NavLink>
```
其中activeClassName默认为**active**，与Bootstrap active高亮一致，若想修改高亮的字体背景颜色，可以自行添加类名，将权重提升到最高（**!important**）

如果我们在进行路由组件的跳转时，如果导航栏较多，就会需要重复写更多的Link组件，那么此时我们可以将其封装
```js
	export default class MyNavLink extends Component {
    render() {
        // console.log(this.props);
        return (
            <NavLink activeClassName="atguigu" className="list-group-item" {...this.props}/>
        )
    }
}
```

```js
<MyNavLink to="/about">About</MyNavLink>
<MyNavLink to="/home">Home</MyNavLink>
```

**注意：** 标签体内容也是特殊的标签属性，为**children** ，所以我们在封装的<NavList>中不用写标签体内容，直接接收props中的属性值即可