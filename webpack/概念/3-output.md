多个入口起点：如果配置创建了多个单独的 "chunk"（例如，使用多个入口起点或使用像 CommonsChunkPlugin 这样的插件），则应该使用 [占位符(substitutions)](https://v4.webpack.docschina.org/configuration/output#output-filename) 来确保每个文件具有唯一的名称。
```js
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
};

// 写入到硬盘：./dist/app.js, ./dist/search.js
```

##  [高级进阶](https://v4.webpack.docschina.org/concepts/output/#%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6)

以下是对资源使用 CDN 和 hash 的复杂示例：

**config.js**

```js
module.exports = {
  //...
  output: {
    path: '/home/proj/cdn/assets/[hash]',
    publicPath: 'http://cdn.example.com/assets/[hash]/'
  }
};
```

如果在编译时，不知道最终输出文件的 `publicPath` 是什么地址，则可以将其留空，并且在运行时通过入口起点文件中的 `__webpack_public_path__` 动态设置。

```js
__webpack_public_path__ = myRuntimePublicPath;

// 应用程序入口的其余部分
```