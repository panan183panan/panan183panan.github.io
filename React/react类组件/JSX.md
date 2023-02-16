关于虚拟DOM：
1.本质是Object类型的对象
2.虚拟DOM比较‘轻’，真实虚拟DOM比较‘重’（虚拟DOM是React内部再用，无需真实DOM有那么多属性）
3.虚拟DOM最终会被React转化为真实DOM呈现在页面上。

jsx: JavaScript XML

jsx语法规则：
1.定义虚拟DOM时，不要写引号
2.标签中混入js表达式需要使用{}
3.样式的类名指定不要用class，要用ClassName
4.内联样式，要用style={{key:value}}
5.只有一个根标签
6.标签必须闭合例如：<input . . . />
7.标签首字母：小写字母转为html中元素，大写字母开头，则渲染React对应的组件。


```html
<div id="test"></div>

<script type="text/babel">
const myId = 'title'
const mydata = 'my name is panan'
  

const VDOM = (
 <h2 id={myId.toLowerCase()}>
 <span>{mydata.toLowerCase()}</span> 
 </h2>
)

ReactDOM.render(
 VDOM,
 document.getElementById('test')
)

</script>
```

动态加载页面：
```html
<div id="test"></div>

<script type="text/babel">

const data=['AAA','BBB','CCC']
const data2=[<li>AAA</li>,<li>BBB</li>,<li>CCC</li>]

const VDOM = (
 <div>
 <h1>前端js框架</h1>
 <ul>
 {
	 data.map((item)=>{
	 return <li>{item}</li>
 })
 }
 </ul> 	
 </div>
)

ReactDOM.render(
 VDOM,
 document.getElementById('test')

)

</script>
```