---
title: JS模块化
date: 2021-10-20
categories: [JavaScript]
---

学习视频：[尚硅谷JS模块化教程](https://www.bilibili.com/video/BV18s411E7Tj)

## 模块化进化史

* 全局function模式

  ```js
  var msg = 'module1'
  function foo () {
      console.log('foo()', msg)
  }
  // foo()
  ```

* namespace模式

  ```js
  let obj = {
  	msg: 'moudule2'
      foo () {
          console.log('foo()', this.msg)
      }
  }
  // obj.foo()
  ```
<!-- more -->
* IIFE模式——匿名函数自调用（闭包）

  ```js
  (function (window) {
      let msg = 'module3'
      function foo () {
          console.log('foo()', msg)
      }
      window.module3 = {foo}
  })(window)
  // module3.foo()
  ```

* IIFE模式增强——引入依赖

  ```js
  (function (window, $) {
      let msg = 'module4'
      function foo () {
          console.log('foo()', msg)
      }
      window.module4 = foo
      $('body').css('background', ' red')
  })(window, jQuery)
  // module4()
  ```

* 造成问题：

  * 请求过多
  * 依赖模糊
  * 难以维护

## 模块化规范

**CommonJS**

* 基本语法
  * 暴露模块  module.exports = value ;  exports.xxx = value
  * 引入模块 require(xxx)
* 实现
  * 服务器端实现 Node.js
  * 浏览器端实现 CommonJs的浏览器端打包工具Browserify

**AMD**

* 说明：Asynchronous Module Definition(异步模块定义)，专门用于浏览器，模块的加载是异步的

* 基本语法

  * 暴露模块 

    ```js
    // 定义没有依赖的模块
    define(function () {
        return 模块
    })
    
    // 定义有依赖的模块
    define(['module1', 'module2'], function (m1, m2) {
        return 模块
    })
    ```

  * 引入模块

    ```js
    requirejs.config({
        baseUrl: '',
        paths: {
          模块名：模块路径
        }
      })
    require(['module1', 'module2'], function(m1, m2) {
        使用m1/m2
    })
    ```

* 实现 [Require.js](https://requirejs.org/)

**CMD**

* 说明：专门用于浏览器端，模块是异步的，使用时才会加载执行

* 基本语法

  * 暴露模块

    ```js
    // 定义没有依赖的模块
    define(function(require, export, module) {
        exports.xxx = value
        module.exports = value
    })
    // 定义有依赖的模块
    define(function (require, export, module) {
        var module2 = require('./module2')
        require.async('./module3', function (m3) {
            
        })
        exports.xxx = value
    })
    ```

  * 引入模块

    ```js
    define(function (require) {
        var m1 = require('./module1')
        var m4 = require('./module4')
        m1.show()
        m4.show()
    })
    ```

* 实现（浏览器端） [Sea.js](https://www.zhangxinxu.com/sp/seajs/)

**ES6**

* 说明：依赖模块需要编译打包出来
* 语法
  * 暴露模块 export
  * 引入模块 import
* 实现（浏览器端）
  * 使用Babel将ES6编译成ES5代码
  * 使用Browserify编译打包js

## ES6（常用）

1.定义package.json文件

```json
{
  "name": "es6_bable-browserify",
  "version": "1.1.0"
}
```

2.安装

```shell
npm install babel-cli browserify -g
npm install babel-reset-se2015 --save-dev
// 引入第三方模块测试 jQuery
npm install jquery@1 --save
```

3.定义.babelrc文件

```json
{
  "presets": ["es2015"]
}
```

4.编码

js/src/module1.js 分别暴露

```js
// 分别暴露
export function foo () {
  console.log('foo() module1')
}
export function bar () {
  console.log('bar() module1')
}
export let arr = [1, 2, 3, 4, 5]
```

js/src/module2.js 统一暴露

```js
// 统一暴露
function fun () {
  console.log('fun() module2')
}
function fun2 () {
  console.log('fun2() module2')
}
export { fun, fun2 }
```

js/src/module3.js 默认暴露

```js
// 默认暴露
// export default () => {
//   console.log('我是默认暴露的')
// }
export default {
  msg: '默认暴露',
  foo () {
    console.log(this.msg)
  }
}
```

js/src/main.js

```js
// import xxx from '路径'
import { foo, arr } from './module1'
import { fun } from './module2'
import module3 from './module3'
import $ from 'jquery'
foo()
console.log(arr)
fun()
module3.foo()
$('body').css('background', 'green')
```

5.编译

* 使用Babel 将ES6编译为ES5代码

  ```shell
  babel js/src -d js/lib
  ```

* 使用Browserify编译js，使包含CommonJS语法的js文件能在浏览器运行

  ```shell
  browserify js/lib/main.js -o js/lib/bundle.js
  ```

6.html页面引入

```html
<script src="./js/dist/bundle.js" type="text/javascript"></script>
```

7.打开html