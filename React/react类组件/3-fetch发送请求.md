fetch与xhr不同，它是浏览器内置，是**原生函数**，基本使用方式为：
```js
fetch(url,options).then(function(response){
	//handle http response
},function(error){
	//handle network error
})
```
**fetch**：（与axios相似，却又不同）,fetch主要是**关注分离**
1. 返回成功的回调中并没有数据，只是代表联系服务器成功了，即使请求地址错误，也会返回相应状态码等。
2. 返回失败的回调更偏向于网络不佳（离线）
我们如何获取成功回调中的数据呢？
![[Pasted image 20220704203221.png]]
我们在成功回调中返回`response.json()`，返回一个promise。

***

	我们根据成功回调的输出，得到fetch返回的是promise格式，（换句话说，就是成功回调中返回的promise中，成功是获取数据成功，失败是资源获取失败，在失败回调返回一般由于离线，没有网络造成）。

```js
fetch('http://xxxxx.xxx').then(
	(response)=>{return response.json},//联系服务器成功
	(error)=>{console.log(error)}//联系服务器失败
).then{
	(response)=>{return response.json},//数据获取成功
	(error)=>{console.log(error)}//数据获取失败
}
```

这样就实现了基本的网络请求，但是它还不够完全准确，我们在promise中可以知道，即使在第一次和服务器取得联系时，我们发现，不管成功与失败，它总是会执行下一步promise的成功回调，所以我们需要再次更改：

```js
fetch('http://xxxxx.xxx').then(
	(response)=>{return response.json},//联系服务器成功
	(error)=>{return new Promise()}//联系服务器失败
).then{
	(response)=>{return response},//数据获取成功
	(error)=>{console.log(error)}//数据获取失败
}
```

接下来，我们可以在对其进行改善，fetch返回产生两个Promise回调，在promise中有方法可以简化其代码：(将失败的回调catch出来，汇总在一个error中)
```js
fetch('http://xxxxx.xxx').then(
	(response)=>{return response.json},//联系服务器成功
	//(error)=>{return new Promise()}//联系服务器失败
).then{
	(response)=>{return response},//数据获取成功
	//(error)=>{console.log(error)}//数据获取失败
}.catch((error)=>{console.log(error)})//失败
```

但是，这并不是最优的，我们可以通过try catch来抓取失败请求，如下所示：
```js
try{
	const response = await fetch(`http://xxxxxx.xxx?a=${keyword}`)
	const data = await response.json()
	console.log(data)
	//消息发布（成功情况
}
catch(error){
	//消息发布（失败情况
	console.log("请求出错",error)
}
```
**注意：await要配合async一起使用，即在函数外面加上async**
```js
search = async()=>{
	const response = await fetch(`http://xxx.xx`)...
}
```

在发送网络请求，有xhr为基础的，以及jQuery和axios，还包括另外的fetch（**fetch的兼容性有点问题，旧版本有点不支持，所以使用率不是很高**）


