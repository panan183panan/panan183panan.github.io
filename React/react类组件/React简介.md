# React简介
React用于构建用户界面的javascript库
1.发送请求数据
2.处理数据（过滤，整理格式）
3.操作DOM呈现过程

为什么学：
1.原生JavaScript操作DOM繁琐，效率低（DOM-API操作UI）
2.使用JavaScript直接操作DOM，浏览器会进行大量的重绘重排
3.原生JavaScript没有组件化编码方案，代码复用率低。

react的特点：
1.采用组件化模式，声明式编码，提高开发效率以及组件复用率。
2.在React Native可以使用React语法进行**移动端开发**
3.使用**虚拟DOM**+优秀的**Diffing**算法，尽量减少与真实DOM的交互

React实现过程：
数据--->虚拟DOM--->真实页面DOM


学习react之前需要掌握的知识
```
判断this的指向
class类
ES6语法规范
npm包
原型，原型链
数组常用方法
模块化
```

# react入门
## 相关js库
1.react.js react核心库
2.react-dom.js 提供操作DOM的react拓展
3.babel.min.js 解析jsx语法代码转换为js代码库

```js
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script> 
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script> 
<script src="https://cdn.staticfile.org/babelstandalone/6.26.0/babel.min.js"></script>
```
react必须在react-dom之前引入

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React!</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>

<div id="root"></div><br />
<div id="t1"></div>
	
<script type="text/babel">

const name1 = 'Josh Perez';
const element1 = <h1>Hello, {name1}</h1>;
ReactDOM.render(
 element1,
 document.getElementById('root')
);

  
function formatName(user) {
 return user.firstName + ' ' + user.lastName;
} 
const user = {
 firstName: 'Harper',
 lastName: 'Perez'
};
const element2 = (
 <h1>
 Hello, {formatName(user)}!
 </h1>
);
ReactDOM.render(
 element2,
 document.getElementById('t1')

);
</script>

</body>
</html>
```

js创建虚拟DOM
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React!</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<!-- <script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script> -->
</head>
<body>

<div id="test"></div><br />

<!-- <script type="text/babel"> -->
<script type="text/javascript">
//创建虚拟DOM
const VDOM = React.createElement('h1',{id:'title'},'Hello, my girl')//可叠加

//渲染DOM到页面
ReactDOM.render(
  VDOM,
  document.getElementById('test')
);


</script>

</body>
</html>
```