## webpack
![[Pasted image 20220227151648.png]]

安装webpack
```
npm install webpack -g
npm install webpack-cli -g

```
安装成功
```
webpack -v

webpack-cli -v

```
![[Pasted image 20220227152900.png]]

## 配置
![[Pasted image 20220227153431.png]]

## 使用webpack
![[Pasted image 20220227153602.png]]

## 安装vue-cli
```
npm install vue-router --save-dev
npm install -g vue-router --save
```



#### 新建项目2
```linux
vue init webpack myvue
```

安装成功
```
webpack -v

webpack-cli -v
```

```
npm install vue-router --save-dev
```
运行后启动报错的使用
```
cnpm install vue-router@3.1.3 --save-dev
```
，那个版本太高了，用不了 ，太坑了，搞了好久

```
npm i element-ui -S
```

```
cnpm install sass-loader node-sass
```

安装webpack
```
npm install webpack -g
```
```
npm install webpack-cli -g
```
安装axios
```
cnpm install anxios -s
npm install --save vue-axios


import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(VueAxios,axios);
```

```
npm install
```

```
npm run dev
```

```shell
npm install npm@3.8.6 -g
```