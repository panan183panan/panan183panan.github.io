**webpack.config.js**
对于**单个**入口，可以简写为
```js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

实际写法为：
```js
module.exports = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};
```

多页面应用程序
```js
module.exports = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```

