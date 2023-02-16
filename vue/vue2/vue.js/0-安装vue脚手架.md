#### 淘宝镜像
```npm
npm config set registry https://registry.npm.taobao.org
```

#### 安装全局脚手架
```npm
 npm install -g @vue/cli
```

##### vue3目前安装element-ui有点问题
![[2{[5%Z5YQ5ZX}({%SER~K58.png]]
#### 创建项目
```npm
 vue create 项目文件夹
```

```
cd 项目文件夹
```

####  安装vue-router
vue2
```shell
npm install --legacy-peer-deps vue-router@3.5.2
```


vue3
```shell
npm i vue-router
```  

#### 安装axios
```shell
npm i axios
```
#### 安装vue-resource
```shell
npm install vue-resource --save
```

#### 安装vuex
```shell
npm i vuex@3
```

#### 安装webpack
```shell
npm install webpack -g
```

```shell
npm install webpack-cli -g
```

#### 安装element--UI

```shell
npm i element-ui -S
```
#### 安装SASS加载器
```shell
npm install sass-loader node-sass
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
 1. 安装pubsub：
```shell
npm i pubsub-js
```
 3. 引入: 
```shell
import pubsub from 'pubsub-js'
```


#### 安装animate.css
```shell
npm install animate.css --save
```
导入文件
```js
import 'animate.css';
```


#### 1. 引入axios时
应该按照以下规则引入
```js

//引入axios  
import axios from 'axios'  
Vue.prototype.axios = axios;


```
#### 2. vue.config.js
```js
lintOnSave:false, //关闭语法检查
```
#### 3. router
```js
new Vue({  
  el: '#app',  
  router ,  
  render: h => h(App)  
});
```
##### router不能忘记写


