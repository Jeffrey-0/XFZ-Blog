---
title: NodeJs基础
date: 2021-3-20
tags: [node]
categories: [后端]
---


课程学习地址

[nodejs(黑马36期)][https://www.bilibili.com/video/av77033948?p=2]



# 1.1Node.js是什么

* Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://v8.dev/).js是构建在以下基础上的JavaScript运行时：[Chrome的V8 JavaScript引擎](https://v8.dev/).
  * Node.js 不是一门语言
  * Node.js 不是库、不是框架
  * Node.js是javascript运行时环境
  * Node.js可以解析和执行JavaScript代码
* 构建与Chrome的v8引擎之上
  * 代码只是具有特定格式的字符串
  * 引擎可以认识它，引擎可以帮你解析和执行
  * Google Chrome 的V8引擎是目前公认解析执行JavaScript的速度最快
  * Node.js 的作者把google Chrome中的v8引擎移植出来，开发了一个独立的JavaScript运行时环境。
* 浏览器中的JavaScript
  * EcmaScript
    * 基本的语法
    * if
    * var
    * function
    * Object
    * Array
  * Bom
  * Dom
* Node.js 中的JavaScript
  * 没有BOM、DOM
  * EcmaScript
  * 在Node这个JavaScript执行环境中为javascript提供了一些服务器级别的操作API
    * 文件读写
    * 网络服务的构建
    * 网络通信
    * http服务器等处理
* Node.js uses an event-driven,non-blocking I/O model that makes it lightweight and efficient.
  * event-driven事件驱动
  * non-blocking I/O model 非阻塞IO模型（异步）
  * lightweight and efficient。轻量和高效
* Node.js' package ecosystem, npm(包管理工具) is the largest ecosystem of  open source libraries in the world.
  * npm是世界上最大的开源库生态系统
  * 绝大多数JavaScript相关的包都存放在npm上，目的是让开发人员方便下载使用。
  * `npm install jquery`
<!-- more -->
# 1.2Node.js 能做什么

* Web服务器后台
* 命令行工具
  * npm
  * git
  * hexo
* 对于前端工程师，接触node最多的是它的命令行工具
  * 自己写的很少，主要是别人第三方写的
  * webpack
  * gulp
  * npm

# 1.3预备知识

* html
* javascript
* css
* 简单的命令行操作
  * cd
  * dir
  * ls
  * mkdir
  * rm
* 具有服务端开发经验更佳

# 1.4 一些资源

* 《深入浅出Node.js》
* 《Node.js权威指南》

# 1.5这门课程能学到啥？

* B/S编程模型
  * Browser-Server
  * back-end
  * 任何服务端技术这种BS编程模型都是一样，和语言无光
  * Node只是作为我们学习BS编程模型的一个工具而已
* 模块化编程
  * RequireJS
  * SeaJS
  * ` @import('文件路径')`
  * 以前认知 的javaScript只能通过script标签来加载
  * 在node中可以像 `@import()`一样来引用加载javascript脚本文件
* Node常用API
* 异步编程
  * 回调函数
  * Promise
  * async
  * generator
* Express Web 开发框架
* Ecmascript 6
  * 只是一个新语法
* 学习Node不仅会帮助大家打开服务端黑盒子，同时会帮助你学习以后的前端高级内容
  * Vue.js
  * React
  * angular

# 2.node中的Javascript

* EcmaScript
* 核心模块
* 第三方模块
* 用户自定义模块

最简单的http服务

```js
// Node构建一个Web服务器
// 在Node中专门提供了一个核心模块：http
// http这个模块的职责就是为你创建编写服务器的


// 1、加载http核心模块
var http = require("http");

// 2、使用http.createServer()方法创建一个web服务器
// 返回一个Server实例
var  server = http.createServer();

// 3、服务器要干嘛
// 提供服务： 对数据的服务
// 发请求
// 接收请求
// 处理请求
// 给个反馈（发送响应）
// 
// 注册 request 请求事件
// 当客户端请求过来，就会自动触发服务器的request请求事件
server.on('request',function(){
	console.log("收到客户端的请求了");
})

//4、绑定端口号，启动服务器
server.listen(3000,function(){
	console.log('服务器启动成功了，可以通过http://127.0.0.1:3000/访问');
})

```

## 2.1核心模块



Node为JavaScript提供了很多服务器级别的API，这些API

绝大多数都被包装到了一个具名的核心模块中了。例如文件操作的`fs`核心模块，http服务构建的`http`模块，`path`路径操作模块、`os`操作系统信息模块

```js
var fs = require('fs')

var http = require('http')
```

## 2.2用户自定义模块

* require
* exports

# 3.Web服务器开发

## 3.1.ip地址和端口号

* ip地址用来定位计算器
* 端口号用来定位具体的应用程序
* 一切需要联网通信的软件都会占用一个端口号
* 端口号的范围从0-65536之间
* 
* 在计算机中有一些默认端口号，最好不要去使用
  * 例如http服务的80
* 我们在开发过程中使用一些简单好记的就可以了，比如3000、5000
* 可以同时开启多个服务，但一定要确保不同服务占用的端口号不一致才可以

## 3.2.Content-Type

* http://tool.oschina.net/

## 3.3.请求对象Request



## 3.4.响应对象Response



## 3.5.在Node中使用模板引擎



## 3.6.统一处理静态资源



## 3.7.服务端渲染



# 4.留言板



# 5.Node中的模块系统

使用Node编写程序主要就是在使用

* EcmaScript语言
  * 和浏览器不一样，在NOde中没有BOM、DOM
* 核心模块
  * 文件操作的fs
  * http服务的http
  * url路径操作模块
  * path路径处理模块
  * os操作系统信息
* 第三方模块
  * art-template
  * 必须通过npm来下载才可以使用
* 咋们自己写的模块
  * 自己创建的文件

## 5.1.什么是模块化

* 文件作用域
* 通信规则
  * 加载
  * 导出

## 5.2.CommonJs模块规范

在Node中的JavaScript还有一个很重要的概念：模块系统

* 模块作用域
* 使用require方法用来加载模块
* 使用exports接口对象用来导出模块中的成员

## 5.2.1. 加载 `require`

```js
var 自定义变量名称 =  require('模块')
```

俩个作用：

* 执行被加载中模块中的代码
* 得到被加载模块中的exports导出接口对象

## 5.2.2. 导出`exports`

* Node中是模块作用域，默认文件中所有的成员只在当前文件模块有效

* 对于希望可以被其他模块访问的成员，我们就需要把这些公开的成员都挂载到exports 接口对象中

  * 导出多个成员（必须在对象中）

    ```js
    exports.自定义变量名 = 对象
    exports.自定义变量名 = 对象
    ```

    

  * 导出单个成员（拿到的就是：函数、字符串）

    ```js
    module.exports = 对象
    ```

## 5.2.3.原理解析

exports 和module.exports的一个引用

```js
exports === module.exports
exports.foo = 'bar'
//等价于
module.exports.foo = 'bar'
```

## 5.2.5.require方法加载规则

* 核心模块

  * 模块名

* 第三方模块

  * 模块名

* 用户自己写的

  * 路径

    

* 优先从缓存中加载

* 判断模块标识

## 5.3.npm

* node package manager

## 5.3.1.npm网站

<http://npmjs.com>

## 5.3.2.npm命令行工具

npm的第二层含义就是一个命令行工具，只要你安装了node就已经安装了npm

npm也有版本这个概念

可以通过在命令行中输入

```
npm --version
```

升级npm

```
npm install --global npm
```

## 5.3.3.常用命令

* npm init
  * npm init -y 可以跳过向导，快速生成
* npm install
  * 一次把dependencies选项中的依赖项全部安装
* npm install 包名
  * 只下载
* npm install --save 包名
  * 下载并且保存依赖项（package.json文件中的dependencies选项）
* npm uninstall 包名
  * 只删除，如果有依赖项依然会保存
  * npm un 包名
* npm uninstall --save 包名
  * 删除的同时也会把依赖信息删除
  * npm un -S 包名
* npm help
  * 查看使用帮助
* npm 包名 --help
  * 查看指定包的使用帮助（可查看缩写）

## 5.3.4.解决npm被墙问题

npm存储包文件的服务器在国外，有时候会被墙，速度很慢，所以我们需要解决这个问题

<http://npm.taobao.org/>淘宝的开发团队把npm在国内做了一个备份

安装淘宝的cnpm

```shell
npm install --global cnpm
```

接下来你安装包的时候把之前的`npm`替换成`cnpm`

```shel
#这里还是走国外的npm服务器，速度比较慢
 npm install  jquery
#使用cnpm 就会通过淘宝的服务器来下载jquery
cnpm install jquery
```

如果不想安装`cnpm`又想使用淘宝的服务器来写

```shell
npm install jquery --registry=https://registry.npm.taobao.org
```

但是每一次手动这样加参数麻烦，所以我们可以吧这个选项假如配置文件中

```shell
npm config set registry https: //registry.npm.taobao.org

#查看npm配置信息
npm config list
```

只要经过上面的命令配置，则你以后所有的`npm install`都会默认通过淘宝的服务器来下载

## 5.4.package.json

我们建议每一个项目都要有一个package.json文件（包描述文件）

这个文件可以通过`npm init`来初始化自动生成

对于我们目前来讲，最有用的是那个`dependencise`选项，可以用来帮我们保存第三方包的依赖信息

如果你的`node_modules`删除了，我们只需要`npm install`就会自动把`package.json`中的`dependencise`中所有的依赖项都下载回来

* 建议每个项目的更目录下都要有一个`package.json`
* 建议执行`npm install 包名 `的时候都要加上`--save`这个选项，目的是用来保存依赖项信息

# 6.Express

原生的http在某些方面表现不足以应对我们的开发需求，所以我们就需要使用框架来加快我们的开发效率，框架的目的就是提高效率，让我们的代码达到高度统一

在Node中，有很多Web开发框架，我们这里以学习`express`为主

* <http://expressjs.com>

## 6.1.起步

#### 6.1.1安装

```shell
npm install -save express
```

#### 6.1.2hello world

```js
var express = require('express')

// 1.创建app
var app = express()

app.get('/', function (req, res) {
	res.send('hello world')
})

app.get('/login', function (req, res) {
	res.send('hello login')
})

app.listen(3000,function () {
	console.log('express app is rnning')
})
```

#### 6.1.3基本路由

路由器

* 请求方法
* 请求路径
* 请求处理函数

get:

```js
app.get('/', function (req, res) {
    res.send('Hello world')
})
```

post:

```js
app.post('/', function (req, res) {
    res.send('Got a Post request')
})
```

#### 6.1.4静态服务

```js
// /public资源
app.use(express.static('public'))

// /files资源
app.use(express.static('files'))

// /public/xxx
app.use('/public',express.static('public'))

// /static/xxx
app.use('/static',express.static('public'))

app.use('/static',express.static(path.jion(__dirname,'public')))
```

### 6.2.在Express中配置art-template模板引擎

安装

```shell
npm install --save art-template
npm install --save express-art-template
```

配置

```js
app.engine('html', require('express-art-template'))
```

使用

```js
app.get('/', function (req, res) {
    //express默认会去项目中的views目录找index.html
    res.render('index.html', {
		title:'hello world'
    })
})
```

如果希望修改默认

```js
app.set('views', 目录路径)
```

### 6.3.在Express中获取表单Get参数

Express内置了一个API，可以直接通过`req.query`来获取

```js
req.query
```

### 6.4.在Express获取表单POST请求体参数

在Express中没有内置获取表单POST请求体的API，这里我们需要使用一个第三方包`body-parser`

安装

```shell
npm install --S body-parser
```

配置

```js
var express = require('express')
var bodyParser = require('body-parser')
var app = express
//配置body-parser
//只要假如这个配置，则在req请求对象上多出来一个属性：body
//可以直接通过req.body 来获取表单PODT请求体数据
app.use(bodyParser.urlencoded({ extended: false}))
app.use(bodyParser.json())
```

使用

```js
app.use(function (req, res) {
    res.setHeader('Content-Type', 'text/plain')
    res.write('you posted:\n')
    res.end(JSON.stringify(req.body,null,2))
})
```



# 7.MongoDb

## 7.1.关系型数据库和非关系型数据库

表就是关系

或者说表和表之间存在关系

* 搜关系型数据库都需要通过sql语言来操作
* 所有的关系型数据库在操作之前就需要设计表结构
* 而且数据表还支持约束
  * 唯一的
  * 主键
  * 默认值
  * 非空
* 非关系型数据库非常灵活
* 有的非关系型数据库就是key - value对儿
* 但是MongoDB是长得最像关系型数据库的非关系型数据库
  * 数据库->数据库
  * 数据表->集合（数组）
  * 表记录->文档对象
* MongoDB不需要设计表结构
* 也就是说你可以任意的往里面存数据，没有结构性这么一说

## 7.2.启动和关闭数据库

启动

```shell
#mongodb 默认使用执行mogod 命令所处盘符根目录下的 /data/db 作为自己的数据库存储目录
#所以在第一次执行该命令之前先自己手动新建一个/data/db
mongod
```

如果想要修改默认的数据存储目录，可以

```shell
mongod --dppath=数据存储目录路径
```

停止

```shell
ctrl+c
```

## 7.3. 连接数据库

连接：

```shell
# 该命令默认连接本机的mongoDB服务
mongo
```

退出：

```shell
# 在连接状态数据exit退出连接
exit
```

## 7.4.基本命令

* `show dbs`
  * 查看显示所有数据库
* `db`
  * 查看当前操作的数据库
* `use 数据库名称`
  * 切换到指定的数据库（如果没有会新建）
* 插入数据
  * `db.students.insert({"name":"Jack"})`

* 查看数据
  * db.students.find()

## 7.5.在node中如何操作mongoDB

### 7.5.1.使用官方的mongoDB包来操作

<https://github.com/mongodb/node-mongodb-native>

### 7.5.2.使用第三方mongoose来操作MongoDB数据库

<http://www.mongoosejs.net/>

## 7.6.mongoose

### 7.6.1.MongoDB数据库的基本概念

* 可以有多个数据库
* 一个数据库可以有多个集合（表）
* 一个集合中可以有多个文档（表记录）
* 文档结构很灵活，没有任何限制
* MongoDB非常灵活，不需要想MySql一样先创建数据库、表、设计表结构
  * 在这里只需要：当你需要插入数据的时候，只需要指定往哪个数据库的哪个集合操作就可以了
  * 一切都由MongoDB来帮你自动完成建库建表这些事

```json
{
    qq : {
        users: [
            {name: '张三' , age: 15},
            {name: '张四' , age: 15},
            {name: '张五' , age: 15},
            {},
            ...
        ],
        products: [
            
        ]
    },
    taobao: {
        
    },
    baidu: {
        
    }
}
```

### 7.6.2.起步

安装：

```shell
npm i mongoose
```

hello world:

```js
const mongoose = require('mongoose');

//连接数据库
mongoose.connect('mongodb://localhost/test');

// 创建一个模型
// 就是在设计数据库
// MongDB是动态的，非常灵活，只需要在代码中设计你的的数据库就可以了
// mongoose这个包就可以让你的设计编写过程变得非常的简单
const Cat = mongoose.model('Cat', { name: String });

// 实例化一个Cat
const kitty = new Cat({ name: 'Zildjian' });

// 持久化保存Kitty实例
kitty.save().then(() => console.log('meow'));
```

### 7.6.3.官方指南

#### 1.设计Scheme发布Model

```js
var mongoose = require('mongoose')

var Schema = mongoose.Schema

// 1连接数据库
mongoose.connect('mongodb://localhost/itcast')

// 2设计集合结构
// 字段名称就是表结构中的属性
// 约束的目的就是为了保证数据的完整性，避免脏数据
var userSchema = new Schema({
	username: {
		type: String,
		required: true //必须有
	},
	password: {
		type: String,
		required: true
	},
	email: {
		type: String
	}
})

// 3.将文档结构发布为模型
//  mongoose.model方法就是用来将一个架构发布为model
//  第一个参数：传入一个大写名称单数字符串用来表示你的数据库名称
//  		mongoose会自动将大写名词的字符串生成小写复数的集合名称
//  		例如这里的User最终会变成users集合名称 
//  第二个参数：架构Schema
//  
//  返回值： 模型构造函数
var User = mongoose.model('User', userSchema)
```

#### 2.增加数据

```js
// 4.当我们有了模型构造函数之后，就可以使用这个构造函数对user集合中的数据
var admin = new User({
	username: 'admin',
	password: '123456',
	email: 'admin@admin.com'
})

admin.save(function (err, ret) {
	if (err) {
		console.log('保存失败')
	} else {
		console.log('保存成功')
		console.log(ret)
	}
})

```

#### 3.查询

查询所有：

```js
User.find(function (err,ret) {
	if (err) {
		console.log('查询失败')
	} else {
		console.log(ret)
	}
})
```

按条件查询所有

```js
User.find({
	username: 'zs'
},function (err,ret) {
	if (err) {
		console.log('查询失败')
	} else {
		console.log(ret)
	}
})
```

按条件查询单个

```js
User.findOne({
	username: 'zs'
},function (err,ret) {
	if (err) {
		console.log('查询失败')
	} else {
		console.log(ret)
	}
})
```

#### 4.删除数据

```js
User.remove({
	username: 'zs'
},function (err, ret) {
	if (err) {
		console.log('删除失败')
	} else {
		console.log('删除成功')
		console.log(ret)
	}
})
```

#### 5.更新数据

```js
User.findByIdAndUpdate('5e7c4f78599c9c1e348345e0',{
	password: '123'
},function (err, ret) {
	if (err) {
		console.log('更新失败')
	} else {
		console.log('更新成功')
	}
})
```

## 7.7.mySql数据库

```js
var mysql      = require('mysql');
//1.创建连接
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : 'root',
  database : 'users' //数据库名称
});
 
 // 2.连接数据库
connection.connect();
 
 // 3.执行数据操作
connection.query('INSERT INTO user VALUES(null,"admin2","123456")', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results);
});
 
 // 4.关闭连接
connection.end();
```



# 8.异步编程

## 8.1.回调函数

不成立的情况

```js
function add(x, y) {
    console.log(1)
    setTimeout(function () {
        console.log(2)
        var ret = x + y
        return ret
    },1000)
    console.log(3)
//到这里执行就结束了，不会等到前面的定时器，所以直接就返回了默认值undefined
}
console.log(add(10, 20))     //undefined
```

回调函数

```js
function add(x, y, callback) {
	console.log(1)
	setTimeout(function () {
		var ret = x + y
		callback(ret)
	},1000)
}

add(10, 20, function (ret) {
	console.log(ret)
})
```

## 8.2.Promise

callback-hell回调地狱

无法保证顺序的代码

```js
var fs = require('fs')
fs.readFile('./data/a.txt', 'utf8', function (err, data) {
	if (err) {
		throw err
	} 
	console.log(data)
})

fs.readFile('./data/b.txt', 'utf8', function (err, data) {
	if (err) {
		throw err
	} 
	console.log(data)
})

fs.readFile('./data/c.txt', 'utf8', function (err, data) {
	if (err) {
		throw err
	} 
	console.log(data)
})
```

通过回调嵌套的方式保证顺序

```js
var fs = require('fs')
fs.readFile('./data/a.txt', 'utf8', function (err, data) {
	if (err) {
		throw err
	} 
	console.log(data)
		fs.readFile('./data/b.txt', 'utf8', function (err, data) {
		if (err) {
			throw err
		} 
		console.log(data)
			fs.readFile('./data/c.txt', 'utf8', function (err, data) {
			if (err) {
				throw err
			} 
			console.log(data)
			})
	})
})
```

为了解决以上编码方式带来的问题（回调地狱嵌套），所以在EcmaScript6中新增一个API`promise`

promise基本语法

```js
// 在Ecmascript6中新增了一个api Promise
// Promise 是一个构造函数

var fs = require('fs')

// 创建一个Promise容器
// 1.给别人一个承诺 I promise you
// Promise本身不是一部，但内部
var p1 = new Promise(function (resolve, reject) {
	fs.readFile('./data/a.txt', 'utf8', function (err, data) {
		if (err) {
			// 把容器的Pending状态变为Rejected
			reject(err)
		} else {
			// 把容器的Pending状态变为Resolved成功
			resolve(data)
		}
	})
})

// p1就是那个承诺
// 当p1成功了，然后then做指定的操作
// then 方法介绍的function就是容器中的resolve函数
p1
	.then(function (data) {
	console.log(data)
	},function (err) {
	console.log('读取失败')
})
```

promise解决异步顺序问题

```js
// 在Ecmascript6中新增了一个api Promise
// Promise 是一个构造函数

var fs = require('fs')

// 创建一个Promise容器
// 1.给别人一个承诺 I promise you
// Promise本身不是一部，但内部
var p1 = new Promise(function (resolve, reject) {
	fs.readFile('./data/a.txt', 'utf8', function (err, data) {
		if (err) {
			// 把容器的Pending状态变为Rejected
			reject(err)
		} else {
			// 把容器的Pending状态变为Resolved成功
			resolve(data)
		}
	})
})

var p2 = new Promise(function (resolve, reject) {
	fs.readFile('./data/b.txt', 'utf8', function (err, data) {
		if (err) {
			// 把容器的Pending状态变为Rejected
			reject(err)
		} else {
			// 把容器的Pending状态变为Resolved成功
			resolve(data)
		}
	})
})

var p3 = new Promise(function (resolve, reject) {
	fs.readFile('./data/c.txt', 'utf8', function (err, data) {
		if (err) {
			// 把容器的Pending状态变为Rejected
			reject(err)
		} else {
			// 把容器的Pending状态变为Resolved成功
			resolve(data)
		}
	})
})



// p1就是那个承诺
// 当p1成功了，然后then做指定的操作
// then 方法介绍的function就是容器中的resolve函数
p1
	.then(function (data) {
	console.log(data)
	// 当p1读取成功时
	// 当前函数中return的结果就可以在后面的then中function接收到
	// 通常return一个Promise对象
	// 当return一个Promise对象的时候，后续的then的参数就是该return对象中的参数
	return p2
	},function (err) {
	console.log('读取失败')
	})	
	.then(function (data) {
		console.log(data)
		return p3
	})
	.then(function (data) {
		console.log(data)
	})
```

封装Promise版本的readFile

```js
var fs = require('fs')

function pReadFile(filePath){
	return new Promise(function (resolve, reject) {
	fs.readFile(filePath, 'utf8', function (err, data) {
		if (err) {
			// 把容器的Pending状态变为Rejected
			reject(err)
		} else {
			// 把容器的Pending状态变为Resolved成功
			resolve(data)
		}
		})
	})
}
pReadFile('./data/a.txt')
	.then(function (data) {
		console.log(data)
		return pReadFile('./data/b.txt')
	})
	.then(function (data) {
		console.log(data)
		return pReadFile('./data/c.txt')
	})
	.then(function (data) {
		console.log(data)
	})
```



# 9.其他

## 9.1.path路径操作模块

* path.basename
  * 获取一个路径的文件名（默认包含扩展名）
* path.dirname
  * 获取一个路径中的目录部分
* path.extname
  * 获取一个路径中的扩展名部分
* path.parse
  * 把一个路径转为对象
    * root 根路径
    * dir目录
    * base包含后缀名的文件名
    * ext后缀名
    * name 不包后缀的文件名
* path.join
  * 当你需要进行路径拼接的时候，推荐使用这个方法
* path.isAbsolute 判断一个路径是否是绝对路径

## 9.2.解决代码写完自动重启服务问题

我们这里可以使用一个第三方命名航工具： `nodemon`来帮我妈解决频繁修改代码重启服务器问题

`nodemon`是一个基于Node.js开发的一个第三方命令行工具

安装

```shell
# 在任意目录执行该命令都可以
npm install --global nodemon
```

检验是否安装成功

```shell
nodemon --version
```



使用

```shell
nodemon app.js
```

只要通过`nodemon app.js`启动的服务，则它会监视你的文件变化，当文件重新保存时会自动帮你重启服务器

## 9.3.文件操作路径和模块路径

文件操作路径

```js
// 在文件操作的相对路径中
// ./data/a.txt	相对于当前目录
// data/a.txt	相对于当前目录
// /data/a.txt	绝对路径，当前文件模块所处磁盘根目录
// c:/xx/xx...	绝对路径
```

模块操作路径

```js
require('./data/foo.js')
//相对于当前目录
require('/data/foo.js')
//绝对路径，当前文件模块所处磁盘根目录
require('data/foo.js')
//错误路径
```

# 10.Node中的其他成员

在每个模块中，处理`require`、`exports`等模块相关API之外，还有俩个特殊成员：

* `dirname`可以用来获取当前文件模块所属目录的绝对路径
* `__filename`可以用来获取当前文件的绝对路径
* 俩者不受node命令所处路径影响的

在文件操作中，使用相对路径是不可靠的，因为在Node中文件操作的路径被设计为相对于执行node命令所处路径（不是bug,人家这样设计是有使用场景的）

所以为了解决这个问题，很简单，只需要把相对路径变成绝对路径就可以了

那这里就可以使用`__dirname`或者`__filename`来帮我们解决这个问题

所以为了尽量避免刚才描述的这个文件，大家以后再文件操作中使用的相对路径都统一转换为动态绝对路径

> 补充：模块中的路径标识和这里的路径没关系，不受影响（相对于文件模块）

