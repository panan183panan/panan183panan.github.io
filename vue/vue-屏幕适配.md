_vue_ _移动端_px_适配_

1.使用lib-flexible动态设置REM基准值(html标签的字体大小)

```
npm i amfe-flexible
然后在main.js引入它
// rem适配
import 'amfe-flexible'
```

 2.使用postcss-pxtorem将px转为rem

```js
// 指定版本安装，安装最新版本会有报错几率
npm i postcss-pxtorem@5.0.0 -D
然后在根目录下创建一个postcss.config.js文件
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-pxtorem': {
      // 设计稿宽除以10，vant以375像素写的
      rootValue: 37.5,
      // 所有属性都会转化
      propList: ['*'],
    },
  },
};
重启服务，刷新页面就可看见效果
```


# **一、lib-flexible**

1.安装

```
npm install lib-flexible --save
```

2.main.js里导入

```
import 'lib-flexible'
```

3.删除index.html里的以下标签，因为lib-flexible会自动添加

```
<meta name="viewport" content="width=device-width,initial-scale=1.0">
```


---

# 二、postcss-plugin-px2rem

postcss-px2rem 全部转换成rem影响UI组件

postcss-px2rem-exclud 只能排除node_module下的文件

安装

```
 npm i postcss-plugin-px2rem --save
```

创建一个名为vue.config.js的文件写入

 下方rootvalue 就先理解为设计稿的尺寸 / 10 就行了,为了么除以10呢,因为flexble里面默认分为10等份,你也可以自行修改平分的份数,这时候的rootvalu就是设计稿 / 你设置的份数

```js
module.exports = {
  css: {
    loaderOptions: {
      postcss: {
        plugins: [
          require('postcss-plugin-px2rem')({
            rootValue: 37.5, // 换算基数，1rem相当于37.5px,值为37.5时,淘宝插件里面为375/10 =37.5
            // unitPrecision: 5, //允许REM单位增长到的十进制数字。
            //propWhiteList: [],  //默认值是一个空数组，这意味着禁用白名单并启用所有属性。
            // propBlackList: [], //黑名单
            exclude: /(node_module)/, //默认false，可以（reg）利用正则表达式排除某些文件夹的方法，例如/(node_module)\/如果想把前端UI框架内的px也转换成rem，请把此属性设为默认值
            // selectorBlackList: [], //要忽略并保留为px的选择器
            // ignoreIdentifier: false,  //（boolean/string）忽略单个属性的方法，启用ignoreidentifier后，replace将自动设置为true。
            // replace: true, // （布尔值）替换包含REM的规则，而不是添加回退。
            mediaQuery: false, //（布尔值）允许在媒体查询中转换px。
            minPixelValue: 3 //设置要替换的最小像素值(3px会被转rem)。 默认 0
          }),
        ]
      }
    }
  }
}
```

## js

```js
(function(doc,win){
    var docEl = doc.documentElement,
    resizeEvt='orientationchange' in window ? 'orientationchange':'resize',
    recalc = function(){
      var clientWidth = docEl.clientWidth;
      if(!clientWidth) return;
      if(clientWidth>750){
        docEl.style.fontSize = '100px'
      }
      else{
        docEl.style.fontSize =  100 * (clientWidth / 750)+'px';
      }
    };
    if(!doc.addEventListener) return;
    win.addEventListener(resizeEvt,recalc,false)
    doc.addEventListener('DOMContentLoaded',recalc,false)
  })(document,window)
```

