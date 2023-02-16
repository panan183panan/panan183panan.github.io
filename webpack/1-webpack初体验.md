开发环境：
	`webpack ./xxx.js -o ./build.js --mode=development`
生产环境：
	`webpack ./xxx.js -o ./build.js --mode=production`

webpack 能处理js/json资源，不能处理css和img等其他资源
生产环境和开发环境将es6模块编译成浏览器能识别的模块化资源
生产环境比开发环境多一个压缩js代码



### webpack.config.js webpack配置文件
```js
//resolve用来拼接绝对路径的方法
const {resolve} = require('path');

module.exports = {
//webpackp配置
	//入口起点
	entry: './src/index.js',
	//输出
	output:{
		//输出文件名，
		filename: 'built.js',
		//输出路径
		//_dirname_nodejs的变量，代表当前文件目录的绝对路径
		path:resolve(__diename,build)
	},
	//loader的配置
	module: {
		rules:{
			//详细的loader配置
			{
				//匹配哪些文件
				test: /\.css$/,
				//使用哪些loader
				use:{
					'style-loader',
					'css-loader',
				}
			}
		}
	},
	//plugins 的配置
	plugins: [
		//详细的plugins设置
	],
	//模式
	mode: 'development'//开发者模式
	//mode: 'production'
}
```










