loader 用于对模块的源代码进行转换。loader 可以使你在 `import` 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript 或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 `import` CSS文件！

[`module.rules`](https://v4.webpack.docschina.org/configuration/module/#module-rules) 允许你在 webpack 配置中指定多个 loader。 这种方式是展示 loader 的一种简明方式，并且有助于使代码变得简洁和易于维护。同时让你对各个 loader 有个全局概览：

loader 从右到左地取值(evaluate)/执行(execute)。在下面的示例中，从 sass-loader 开始执行，然后继续执行 css-loader，最后以 style-loader 为结束。查看 [loader 功能](https://v4.webpack.docschina.org/concepts/loaders/#loader-features) 了解有关 loader 顺序的更多信息。
```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          },
          { loader: 'sass-loader' }
        ]
      }
    ]
  }
};
```

###  [内联(inline)](https://v4.webpack.docschina.org/concepts/loaders/#%E5%86%85%E8%81%94-inline-)

可以在 `import` 语句或任何 [等同于 "import" 的方法](https://v4.webpack.docschina.org/api/module-methods) 中指定 loader。使用 `!` 将资源中的 loader 分开。每个部分都会相对于当前目录解析。

```js
import Styles from 'style-loader!css-loader?modules!./styles.css';
```

使用 `!` 为整个规则添加前缀，可以覆盖配置中的所有 loader 定义。

选项可以传递查询参数，例如 `?key=value&foo=bar`，或者一个 JSON 对象，例如 `?{"key":"value","foo":"bar"}`。

###  [CLI](https://v4.webpack.docschina.org/concepts/loaders/#cli)

还可以通过 CLI 使用 loader：

```js
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
```

这会对 `.jade` 文件使用 `jade-loader`，以及对 `.css` 文件使用 [`style-loader`](https://v4.webpack.docschina.org/loaders/style-loader) 和 [`css-loader`](https://v4.webpack.docschina.org/loaders/css-loader)

####  [loader 特性](https://v4.webpack.docschina.org/concepts/loaders/#loader-%E7%89%B9%E6%80%A7)

-   loader 支持链式传递。链中的每个 loader 会将转换应用在已处理过的资源上。一组链式的 loader 将按照相反的顺序执行。链中的第一个 loader 将其结果（也就是应用过转换后的资源）传递给下一个 loader，依此类推。最后，链中的最后一个 loader，返回 webpack 期望 JavaScript。
-   loader 可以是同步的，也可以是异步的。
-   loader 运行在 Node.js 中，并且能够执行任何 Node.js 能做到的操作。
-   loader 可以通过 `options` 对象配置（仍然支持使用 `query` 参数来设置选项，但是这种方式已被废弃）。
-   除了常见的通过 `package.json` 的 `main` 来将一个 npm 模块导出为 loader，还可以在 module.rules 中使用 `loader` 字段直接引用一个模块。
-   插件(plugin)可以为 loader 带来更多特性。
-   loader 能够产生额外的任意文件。

通过（loader）预处理函数，loader 为 JavaScript 生态系统提供了更多能力。 用户现在可以更加灵活地引入细粒度逻辑，例如：压缩、打包、语言翻译和 [更多其他特性](https://v4.webpack.docschina.org/loaders)。

#### [解析 loader](https://v4.webpack.docschina.org/concepts/loaders/#%E8%A7%A3%E6%9E%90-loader)
loader 遵循 [模块解析](https://v4.webpack.docschina.org/concepts/module-resolution/) 标准。多数情况下，loader 将从 [模块路径](https://v4.webpack.docschina.org/concepts/module-resolution/#module-paths) 加载（通常是从 `npm install`, `node_modules` 进行加载）。
通常使用 npm 进行管理，但是也可以将自定义 loader 作为应用程序中的文件。按照约定，loader 通常被命名为 `xxx-loader`（例如 `json-loader`）