学习vue我们必须之到它的7个属性，8个 方法，以及7个指令。787原则

-   el属性
    用来指示vue编译器从什么地方开始解析 vue的语法，可以说是一个占位符。

-   data属性
    用来组织从view中抽象出来的属性，可以说将视图的数据抽象出来存放在data中。

-   template属性
    用来设置模板，会替换页面元素，包括占位符

-   methods属性
    放置页面中的业务逻辑，js方法一般都放置在methods中
-   render属性
    创建真正的Virtual Dom

-   computed属性
    用来计算
-   watch属性
    watch:function(new,old){}
    监听data中数据的变化
    两个参数，一个返回新值，一个返回旧值，
```html
<div id="app">
    {{msg}}
      <div>这是模板的第一种使用方法1</div>
</div>
  
<template id="bot">这是模板的第三种使用方法，不常用3</template>
<script>
<div id="bot">模板的第四种创建方法4</div>
</script>
<script>
    var vm1 = new Vue({
        data: {
            msg: "data属性"
        },
        methods: {
            Personal:function () {
                console.log("methods方法存放方法")
            }
        },
        template: `<div>模板的第二种使用方法2</div>`,
        //template："#bot",
        render: (createElement) => {
            return createElement("h1",{"class":"类名"，"style":"color: red"},"这一个render属性创建的虚拟dom")
        },
    })
</script>
```
### methods和computed其中都可以写算法，有什么区别呢？
```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<title>Title</title>  
<script src="javascript![](file:///C:\Users\asus\AppData\Roaming\Tencent\QQTempSys\[LC3U)F{0XCAB)LKNIT0K@G.gif)ue.min.js"></script>  
</head> <body>  
<div id="app">  
    <p>{{message}}</p> //直接在模板中绑定表达式  
    <p>{{message.split('').reverse().join('')}}</p> //运用计算属性  
    <p>{{reverseMessage}}</p> //运用methods方式  
    <p>{{methodMessage()}}</p>  
</div>  
<script>  
    var vm=new Vue({  
         el:"#app",  
         data:{  
             message:"hello"  
         },  
        computed:{  
            reverseMessage:function(){  
                 return this.message.split('').reverse().join('');  
            }  
        },  
         methods:{  
             methodMessage:function () {  
                 return this.message.split('').reverse().join('');  
             }  
         }  
    })  
</script>  
</body>  
</html>
```