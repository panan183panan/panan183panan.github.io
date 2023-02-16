```js
/**

 * 封装一个函数 mineReadFile 读取文件内容

 * 参数:  path  文件路径

 * 返回:  promise 对象

 */

function mineReadFile(path){

 return new Promise((resolve, reject) => {

 //读取文件

 require('fs').readFile(path, (err, data) =>{

 //判断

 if(err) reject(err);

 //成功

 resolve(data);

 });

 });

}

  

mineReadFile('./代码/1-Promise基本使用/resource/content.txt')

.then(value=>{

 //输出文件内容

 console.log(value.toString());

}, reason=>{

 console.log(reason);

});
```

## 封装原理
	将函数传入参数，将参数带入promise，并返回（return），在通过调用函数mineReadFile().then(value=>{},reason=>{})进行回调。得到两种状态下的不同结果。


