## 什么是MVVM
	MVVM（Model View View Model）是一种软件架构模式，一种简化用户界面的事件驱动编程方式。MVVM源于经典的MVC（Model View Controller）模式。MVVM的核心是ViewModel层，负责转换MOdel中的数据对象来让数据变得更加容易管理和使用。作用如下：
1. 该层向上与视图层进行双向数据绑定
2. 向下与Model层通过接口请求数据交互（当下流行的MVVM框架有：Vuejs，AngularJS等）
![[Pasted image 20220225210433.png]]

## 为什么使用MVVM
1. **低耦合**：视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的View上，当view变化的时候model可以不变，model变化的时候view也可以不变。
2. **可复用**：可以把逻辑视图放在一个viewmodel里面，让很多view重用这段逻辑视图。
3. **独立开发**：开发人员可以专注于业务逻辑和数据的开发，设计人员可以专注于页面设计。
4. **可测试**：界面素来是比较难以测试的，而现在测试的可以针对ViewModel来写。
![[Pasted image 20220225211937.png]]

## vue语法
### v-bind


## 组件
![[Pasted image 20220226145504.png]]

## 插槽
![[Pasted image 20220227103548.png]]

## 自定义内容与事件分发
![[Pasted image 20220227110714.png]]
![[Pasted image 20220227105714.png]]
![[Pasted image 20220227105721.png]]
![[Pasted image 20220227132852.png]]
### 说明：
	Vue的开发都是基于Nodejs，实际开发采用vue-cli脚手架开发，vue-router路由，vuex做状态管理，VueUI，界面我们一般使用ElementUI（饿了么出品），或者ICE（阿里巴巴出品）来快速搭建前端项目

 vue中数据和页面分开操作

计时器：只有加减功能
```html
<div id="app">  
 <h2>当前计数：{{counter}}</h2>  
 <button v-on:click="counter++">+</button>  
 <button v-on:click="counter--">-</button>  
</div>  
  
  
<script src="../js/vue.min.js"></script>  
<script>  
 //let (变量),const(常量)  
 const app = new Vue({  
        el: '#app', //挂载要管理的元素  
 data: {//定义数据  
 counter:0  
 }  
    })  
  
</script>
```

函数式计时器：
methods：定义函数方法
@click：v-on:click 监听事件
```html
<div id="app">  
 <h2>当前计数：{{counter}}</h2>  
<!--    <button v-on:click="counter++">+</button>-->  
<!--    <button v-on:click="counter&#45;&#45;">-</button>-->  
  
 <button @click="add">+</button>  
 <button @click="sub">-</button>  
</div>  
  
<script src="../js/vue.min.js"></script>  
<script>  
 //let (变量),const(常量)  
 const app = new Vue({  
        el: '#app', //挂载要管理的元素  
 data: {//定义数据  
 counter:0  
 },  
 methods:{  
            add : function (){  
                console.log("add被执行");  
 this.counter++;  
 },  
 sub : function (){  
                console.log("sub被执行");  
 this.counter--;  
 }  
        }  
    })  
  
</script>
```

## vue基本模板语法

- Mustache（双大括号）
不仅仅可以直接写变量，还可以写一写简单的表达式

- v-once的使用
只在第一次显示数据，其他时候不会变

- v-html
```html
url='<a hef="http://ww.baidu.com"></a>'

<h2 v-html>{{url}}</h2>
```


```js
//升降排序
if(this.sortType){  
   arr.sort((p1,p2)=>{  
      return this.sortType === 1 ? p2.age-p1.age : p1.age-p2.age  
 })  
}
```

```js

//更新信息
this.persons.splice(0,1,{id:'001',name:'马老师',age:50,sex:'男'})
```

```js
addSex(){  
   // Vue.set(this.student,'sex','男')  
 this.$set(this.student,'sex','男')  
},  
addFriend(){  
   this.student.friends.unshift({name:'jack',age:70})  
},  
updateFirstFriendName(){  
   this.student.friends[0].name = '张三'  
},  
addHobby(){  
   this.student.hobby.push('学习')  
},  
updateHobby(){  
   // this.student.hobby.splice(0,1,'开车')  
 // Vue.set(this.student.hobby,0,'开车')  
 this.$set(this.student.hobby,0,'开车')  
},  
removeSmoke(){  
   this.student.hobby = this.student.hobby.filter((h)=>{  
      return h !== '抽烟'  
 })  
}
```


```js
我们学过的指令：  
 v-bind : 单向绑定解析表达式, 可简写为 :xxx v-model    : 双向数据绑定  
 v-for      : 遍历数组/对象/字符串  
 v-on       : 绑定事件监听, 可简写为@  
 v-if      : 条件渲染（动态控制节点是否存存在）  
 v-else     : 条件渲染（动态控制节点是否存存在）  
 v-show     : 条件渲染 (动态控制节点是否展示)  
 v-text指令：  
 1.作用：向其所在的节点中渲染文本内容。  
 2.与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。  


 v-html指令：  
 1.作用：向指定节点中渲染包含html结构的内容。  
 2.与插值语法的区别：  
 (1).v-html会替换掉节点中所有的内容，{{xx}}则不会。  
 (2).v-html可以识别html结构。  
 3.严重注意：v-html有安全性问题！！！！  
 (1).在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。  
 (2).一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！


v-cloak指令（没有值）：  
 1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。  
 2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。


v-pre指令：  
 1.跳过其所在节点的编译过程。  
 2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。


需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。  
需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。  
 自定义指令总结： 一、定义语法：  
 (1).局部指令：  
 new Vue({                                            new Vue({ directives:{指令名:配置对象} 或 directives{指令名:回调函数}  
 })                                                        }) 
(2).全局指令：  
 Vue.directive(指令名,配置对象) 或 Vue.directive(指令名,回调函数)  
  
 二、配置对象中常用的3个回调：  
 (1).bind：指令与元素成功绑定时调用。  
 (2).inserted：指令所在元素被插入页面时调用。  
 (3).update：指令所在模板结构被重新解析时调用。  
  
 三、备注：  
 1.指令定义时不加v-，但使用时要加v-；  
 2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。  


生命周期：  
 1.又名：生命周期回调函数、生命周期函数、生命周期钩子。  
 2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。  
 3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。  
 4.生命周期函数中的this指向是vm 或 组件实例对象。


 常用的生命周期钩子：  
 1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。  
 2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。  
  
关于销毁Vue实例  
 1.销毁后借助Vue开发者工具看不到任何信息。  
 2.销毁后自定义事件会失效，但原生DOM事件依然有效。  
 3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。


Vue中使用组件的三大步骤：  
 一、定义组件(创建组件)  
 二、注册组件  
 三、使用组件(写组件标签)  
  
一、如何定义一个组件？  
 使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；  
 区别如下：  
 1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。  
 2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。  
 备注：使用template可以配置组件结构。  
  
二、如何注册组件？  
 1.局部注册：靠new Vue的时候传入components选项  
 2.全局注册：靠Vue.component('组件名',组件)  
  
三、编写组件标签：  
 <school></school>

几个注意点：  
 1.关于组件名:  
 一个单词组成：  
 第一种写法(首字母小写)：school  
 第二种写法(首字母大写)：School  
 多个单词组成：  
 第一种写法(kebab-case命名)：my-school  
 第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持)  
 备注：  
 (1).组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。  
 (2).可以使用name配置项指定组件在开发者工具中呈现的名字。  
  
 2.关于组件标签:  
 第一种写法：<school></school>  
 第二种写法：<school/>  
 备注：不用使用脚手架时，<school/>会导致后续组件不能渲染。  
  
 3.一个简写方式：  
 const school = Vue.extend(options) 可简写为：const school = options


关于VueComponent：  
 1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。  
  
 2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，  
 即Vue帮我们执行的：new VueComponent(options)。  
  
 3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！  
  
 4.关于this指向：  
 (1).组件配置中：  
 data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。  
 (2).new Vue(options)配置中：  
 data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。  
  
 5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。  
 Vue的实例对象，以后简称vm。

```
1.一个重要的内置关系：VueComponent.prototype.__proto__ === Vue.prototype  
2.为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。


进行数据统计：得到符合要求的数据

```js
 //此处使用reduce方法做条件统计

 const x = this.todos.reduce((pre,current)=>{

	 console.log('@',pre,current)
	
	 return pre + (current.done ? 1 : 0)

 },0) 

 //简写

 return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
```

