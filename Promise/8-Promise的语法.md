```html
<!DOCTYPE html>

<html lang="en">

<head>

 <meta charset="UTF-8">

 <meta name="viewport" content="width=device-width, initial-scale=1.0">

 <title>Promise API</title>

</head>

<body>

 <script>

 //

 let p = new Promise((resolve, reject) => {

 // ** 同步调用

 // console.log(111);

 //修改 promise 对象的状态

 reject('error');

 });

  

 // console.log(222);

  

 //执行 catch 方法

 p.catch(reason => {

 console.log(reason);

 });

 </script>

</body>

</html>
```

#### catch函数：
只能在失败状态中执行catch函数，得到失败原因

#### Promise.all
包含n个Promise 对象，当全部的Promise返回正确时，Promise才会正确，反之只要有一个错误就说明Promise返回错误。

#### Promise.race
 返回一个新的promise，第一个完成的promise的结果状态就是最终的结果状态

#### promise异常穿透
1. 当使用promise的then链式调用时，可以在最后指定失败的回调
2. 前面任何操作出现了异常，都会传到最后失败的回调中处理

#### 自定义封装Promise，
```js
//声明构造函数

function Promise(executor){

 //添加属性

 this.PromiseState = 'pending';

 this.PromiseResult = null;

 //保存实例对象的 this 的值

 const self = this;// self _this that

 //resolve 函数

 function resolve(data){

 //1. 修改对象的状态 (promiseState)

 self.PromiseState = 'fulfilled';// resolved

 //2. 设置对象结果值 (promiseResult)

 self.PromiseResult = data;

 }

 //reject 函数

 function reject(data){

 //1. 修改对象的状态 (promiseState)

 self.PromiseState = 'rejected';//

 //2. 设置对象结果值 (promiseResult)

 self.PromiseResult = data;

 }

 //同步调用『执行器函数』

 executor(resolve, reject);

}

//添加 then 方法

Promise.prototype.then = function(onResolved, onRejected){ 

}
```

#### 抛出错误
```js
 try{

 //同步调用『执行器函数』

 executor(resolve, reject);

 }catch(e){

 //修改 promise 对象状态为『失败』

 reject(e);

 }
```

#### 状态只能修改一次
```js
//声明构造函数

function Promise(executor){

 //添加属性

 this.PromiseState = 'pending';

 this.PromiseResult = null;

 //保存实例对象的 this 的值

 const self = this;// self _this that

 //resolve 函数

 function resolve(data){

 //判断状态

 ----if(self.PromiseState !== 'pending') return;

 //1. 修改对象的状态 (promiseState)

 self.PromiseState = 'fulfilled';// resolved

 //2. 设置对象结果值 (promiseResult)

 self.PromiseResult = data;

 }

 //reject 函数

 function reject(data){

 //判断状态

 ----if(self.PromiseState !== 'pending') return;

 //1. 修改对象的状态 (promiseState)

 self.PromiseState = 'rejected';//

 //2. 设置对象结果值 (promiseResult)

 self.PromiseResult = data;

 }

 try{

 //同步调用『执行器函数』

 executor(resolve, reject);

 }catch(e){

 //修改 promise 对象状态为『失败』

 reject(e);

 }

}

  

//添加 then 方法

Promise.prototype.then = function(onResolved, onRejected){

  

}
```

#### then方法执行回调
```js
//添加 then 方法

Promise.prototype.then = function(onResolved, onRejected){

 //调用回调函数  PromiseState

 if(this.PromiseState === 'fulfilled'){

 onResolved(this.PromiseResult);

 }

 if(this.PromiseState === 'rejected'){

 onRejected(this.PromiseResult);

 }

}
```

#### 异步任务then执行回调
```js
//声明构造函数

function Promise(executor){

 //添加属性

 this.PromiseState = 'pending';

 this.PromiseResult = null;

 //声明属性

 this.callback = {};

 //保存实例对象的 this 的值

 const self = this;// self _this that

 //resolve 函数

 function resolve(data){

 //判断状态

	 if(self.PromiseState !== 'pending') return;

 //1. 修改对象的状态 (promiseState)

	 self.PromiseState = 'fulfilled';// resolved

 //2. 设置对象结果值 (promiseResult)

	 self.PromiseResult = data;

 //调用成功的回调函数

	 if(self.callback.onResolved){
	
		 self.callback.onResolved(data);

	 }

 }

 //reject 函数

 function reject(data){

 //判断状态

		 if(self.PromiseState !== 'pending') return;

 //1. 修改对象的状态 (promiseState)

		 self.PromiseState = 'rejected';//

 //2. 设置对象结果值 (promiseResult)

		 self.PromiseResult = data;

 //执行回调

		 if(self.callback.onResolved){

			 self.callback.onResolved(data);

		 }
	
	 }

	 try{

 //同步调用『执行器函数』

		 executor(resolve, reject);

	 }catch(e){

 //修改 promise 对象状态为『失败』

		 reject(e);
	
	 }

}

  

//添加 then 方法

Promise.prototype.then = function(onResolved, onRejected){

 //调用回调函数  PromiseState

 if(this.PromiseState === 'fulfilled'){

	 onResolved(this.PromiseResult);

 }

 if(this.PromiseState === 'rejected'){

	 onRejected(this.PromiseResult);

 }

 //判断 pending 状态

 if(this.PromiseState === 'pending'){

 //保存回调函数

	 this.callback = {
	
		 onResolved: onResolved,
		
		 onRejected: onRejected
		
		 }
	
	}
}
```

