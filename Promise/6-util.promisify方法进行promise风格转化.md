```js
/**

 * util.promisify 方法

 */

//引入 util 模块

const util = require('util');

//引入 fs 模块

const fs = require('fs');

//返回一个新的函数

let mineReadFile = util.promisify(fs.readFile);
mineReadFile('./代码/1-Promise基本使用/resource/content.txt').then(value={
	console.log(value.toString());
});

```

内置函数，使用起来更加方便