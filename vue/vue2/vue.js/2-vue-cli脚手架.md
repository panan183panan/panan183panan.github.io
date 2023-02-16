vue-cli脚手架是官方提供的，用于快速生成一个vue的项目模板。

预先定义好的目录的结构以及基础代码，就好比我们在创建Maven项目时可以选择创建一个骨架项目，这个骨架项目就是脚手架，我们的开发更加快速。	
## 主要功能：
1. 统一的目录结构
2. 本地调试
3. 热部署
4. 单元测试
5. 集成打包上线 

安装nodejs、安装cnpm，安装全局vue


您应该能够简单地更新警告消息中请求的 core-js 模块的版本：
```
npm install --save core-js@^3
```
对于它的价值，npm 有一个漂亮的功能，可以让你查看哪些包已经
```
npm outdated
```


## 安装vue-cli

#### 新建项目
淘宝镜像
```npm
npm config set registry https://registry.npm.taobao.org
```

安装全局脚手架
```npm
 npm install -g @vue/cli
```

创建项目
```npm
 vue create 项目文件夹
```

```
cd 项目文件夹
```

开启服务
```npm
npm run serve
```


在vue.config.js更改为：
```js
const { defineConfig } = require('@vue/cli-service')  
module.exports = defineConfig({  
  // transpileDependencies: true  
//关闭语法检查
 lintOnSave: false  
})
```


#### 安装pubsub.js
 1. 安装pubsub：```npm i pubsub-js```
 2. 引入: ```import pubsub from 'pubsub-js'```


#### 安装animate.css
```shell
npm install animate.css --save
```
导入文件
```js
import 'animate.css';
```


或者
```html
<head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"
  />
</head>
```

#### 安装axios
```shell
npm i axios
```

#### 搭建vuex环境
![[Pasted image 20220311115349.png]]
##### 安装vuex
	注意：2022年2月7日之后，vue3成为了默认版本，直接执行`npm i vuex`，直接安装vue3了，vue3成为了默认版本的同时，vuex也更新到了4版本。
	vue2中只能用vue3的版本，vue3中只能用vuex4的版本。
	所以我们要指定安装vuex的版本号：

```shell
npm i vuex@3
```

导入vuex包：
```shell
import Vuex from 'vuex'

Vue.use(Vuex)

//然后就可以在开始main.js中传入store
```

##### vuex标准模式：
在src下创建store文件夹，创建index.js。
```js
//该文件用于创建Vuex中最为核心的store
import Vue from 'vue'

//引入Vuex
import Vuex from 'vuex'

//应用Vuex插件
Vue.use(Vuex)

//准备actions——用于响应组件中的动作
const actions = {}

//准备mutations——用于操作数据（state）
const mutations = {}

//准备state——用于存储数据
const state = {}

//创建并暴露（导出）store
export default new Vuex.Store({
	 actions,
	 mutations,
	 state,
})	
```
main.js引入store：
```js
import store from './store'//未写具体的，默认index.js

//在创建store之前必须要先Vue.use(vuex);

//vue脚手架在执行渲染的时候，优先将所有的import导入的优先执行，然后在执行其他事件。所以我们将vue写在store下的index.js里面
```


#### store中getters的配置项：
![[Pasted image 20220311201355.png]]

getters拿着state中的数据进行加工处理，并返回。



####  mapState与mapGetters
```js
import {mapState，mapGetters} from 'vuex'

conputed(){
	...mapState({he:'sum',xuexiao:'school'})//...为es6的语法，可以将里面的每一项展开显示出来
		//当变量和属性名要一致！！
	...mapState(['sum','school'])
	...mapGetters(['bingSum'])
}

mounted(){
	const x = mapState({he:'sum',xuexiao:'school'})
}
```

api测试网址：

```1
https://api.github.com/search/users?q=XXX

```

```1
https://api.uixsj.cn/hitokoto/get?type=social
```

####  安装vue-route
```shell
npm i vue-router
```  




