---
title: Webpack4基础
date: 2021-10-8
tags: [webpack]
categories: [打包器]
---


学习视频: [10天搞定webpack4](https://www.bilibili.com/video/BV1a4411e7Bz?p=2)

## webpack安装
```shell
npm i webpack webpack-cli -D
```

## 执行
```shell
npx webpack
```

## webpack 可以0配置
- 打包工具 -> 输出后的结果(js模块)
- 打包（支持js的模块化）
<!-- more -->
## 手动配置
```js
// flie:webpack.config.js
let path = require('path')
module.exports = {
  mode: 'development', // 模式
  entry: './src/index.js', // 入口
  output:{
    filename: 'bundle.js', //打包后的文件名
    path: path.resolve(__dirname, 'dist'), //路径必须是一个绝对路径
  }
}
```

## 快捷运行
1. 在`package.json`中配置快捷命令
    ```
    // file:package.json
    "scripts": {
    "build": "webpack --config webpack.config.js"
    }
    ```
2. 在命令行中运行命令
    ```shell
    npm run build
    ```
ps: 如果要在后面加入参数，在命令中添加 --

## 开启静态服务器插件

> 插件`webpack-dev-server`,模拟服务器，在内存中打包，并不会实际生成
- 安装`npm i webpack-dev-server -D`

- 运行`npx webpack-dev-server`

- 打开`http://localhost:8080/`(默认)

- 配置

  ```js
  // file：webpack.config.js
  devServer: { // 开发服务器的配置
      port: 3000,
      progress: true,
      contentBase: './build',
      compress: true
  }
  ```


## 默认导入页面插件

> 插件`html-webpack-plugin`,设置生成的js要插入哪个页面

* 安装`npm i html-webpack-plugin -D`

* 配置

  ```js
  // file: webpack.config.js
  plugins:[ //数组：放着所有webpack插件
      new HtmlWebpackPlugin({
        template: './src/index.html',  // 入口页面
        filename: 'index.html',   // 输出页面名称
        minify: {
          removeAttributeQuotes:true,  // 去除属性双引号
          collapseWhitespace: true, // 去除空格
        },
        hash: true // 增加后缀
      })
    ]
  ```

## 样式处理

### 样式压缩

> 插件：`css-loader`,`style-loader`,`less-loader`

安装：`npm i css-loader style-loader less-loader -D`

配置

```js
// file: webpack.config.js
  module: { //模块
    rules: [ 
    // 规则 css-loader 解析@import这种语法的
    // style-loader 把css插入到head的标签中
      { test: /\.css$/,
        use: [
        {
          loader: 'style-loader'
          }
        },
        'css-loader'
        ]
      },
      { test: /\.less$/,
        use: [
        {
          loader: 'style-loader',
        },
        'css-loader',
        'less-loader'
        ]
      }
  }
```

### 样式抽离

> 插件 `mini-css-extract-plugin`

安装 `npm i mini-css-extract-plugin -D`

引入 

```js
let MiniCssExtractPlugin = require('mini-css-extract-plugin')
```

新建对象

```
plugins:[ //数组：放着所有webpack插件
    new MiniCssExtractPlugin({
      filename: 'main.css'
    })
  ]
```

配置

```js
module: { 
    rules: [
      {
        test: /\.css$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader'
        ]
      },
      {
        test: /\.less$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          'less-loader'
        ]
      }
    ]
  }
```

### 加样式前缀

> 插件postcss-loader autoprefixer

安装 `npm i postcss-loader  autoPrefixer -D`

**配置**

新建配置文件`postcss.config.js`

```js
// file: postcss.config.js
module.exports = {
  plugins: [require('autoprefixer')]
}
```

在`package.json`中添加浏览器配置

```json
// file:package.json
"browserslist": [
      "defaults",
      "not ie < 11",
      "last 2 versions",
      "> 1%",
      "iOS 7",
      "last 3 iOS versions"
    ]
```

在样式抽离例子基础上，在css-loader之后增加`postcss-loader`

```js
 use: [
     MiniCssExtractPlugin.loader,
     'css-loader',
     'postcss-loader',
     'less-loader'
 ]
```

### 文件压缩(css+js)

> 插件`optimize-css-assets-webpack-plugin`  `terser-webpack-plugin`

安装`npm i optimize-css-assets-webpack-plugin terser-webpack-plugin -D`

引入

```js
let OptimizeCss = require('optimize-css-assets-webpack-plugin')
let TerserJSPlugin = require('terser-webpack-plugin')
```

配置

```js
optimization:{ // 优化项
    minimizer:[
      new TerserJSPlugin({}),
      new OptimizeCss()
    ]
  },
```

## es6->es5

> 插件 `babel-loader`、 `@babel/core`、 `@babel/preset-env`

安装`npm i babel-loader @babel/core @babel/preset-env -D`

配置

```js
module: { //模块
    rules: [
      {
        test: /.js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              '@babel/preset-env'
            ]
          }
        }
      }
    ]
}
```

