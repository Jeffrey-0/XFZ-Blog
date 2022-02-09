---
title: WebSocket全双工通信
date: 2021-7-25
tags: [webSocket]
categories: [通信]
---

学习课程: [3小时教你如何使用websocket实现一个聊天室](https://www.bilibili.com/video/BV1yi4y1t7yD)
> WebSocket协议是基于TCP的一种新的网络协议，实现了浏览器和服务器全双工(full-duplex)通信——允许服务器主动发送信息给客户端
> WebSocket是一种持久的协议，http是非持久协议

早期没有websocket时，通过ajax轮询，由于http请求，服务器无法给浏览器主动发送数据，因此需要浏览器定时给服务器发送请求，服务器把最新的数据响应给浏览器。这种模式的缺点就是浪费性能和资源。



## WebSocket基本使用
在HTML5中，浏览器已经实现了websocket的API，可直接使用

**创建websocket对象**

  ```js
// 演示websoket在浏览器如何使用
// H5已经提供了websocket的API，所以我们可以直接使用

// 1.创建websocket
// 参数1： websocket的服务地址
// 参数2：protocol可选，指定连接的协议
// var socket = new WebSocket('ws://echo.websocket.org')
    var socket = new WebSocket(url, [protocol])
  ```

**websocket事件**

| 事件    | 事件处理程序     | 描述()               |
| ------- | ---------------- | -------------------- |
| open    | Socket.onopen    | 连接建立触发         |
| message | Socket.onmessage | 客户端接收服务器数据 |
| error   | Socket.onerror   | 通信发生错误         |
| close   | Socket.onclose   | 连接关闭触发         |

**websocket方法**

| 方法           | 描述             |
| -------------- | ---------------- |
| Socket.send()  | 使用连接发送数据 |
| Socket.close() | 关闭连接         |
<!-- more -->

**实例**
```js
// 1.创建websocket
// 参数1： websocket的服务地址
var socket = new WebSocket('ws://echo.websocket.org')
// var socket = new WebSocket('ws://localhost:3000')

// 2.open:当和websocket服务器连接成功时触发
socket.addEventListener('open', () => {
  div.innerHTML = '连接服务器成功'
})

// 3.主动给websocket服务器发送消息
button.addEventListener('click', () => {
  var value = input.value
  socket.send(value)
})

// 4.接收websocket服务的数据
socket.addEventListener('message', (message) => {
  console.log(message)
  div.innerHTML=message.data
})
```

## 使用nodejs开发websocket服务

**实例**

```js
// 1.导入nodejs-websocket包
const ws = require('nodejs-websocket')
const PORT = 3000

// 2.创建一个server
// 2.1如何处理用户的请求

// 每次只要有用户连接，函数就会被执行，会给当前连接的用户创建一个connect对象
const server = ws.createServer(connect => {
  console.log('用户连接上来了')
  // 每当接收到用户传递过来的数据，这个text事件就会被触发
  connect.on('text', data => {
    console.log('接收到用户的数据', data)
    // 给用户一个响应的数据
    connect.send(data.toUpperCase() + '!!!')
  })
  // 只要websocket连接断开了，close事件就会触发
  connect.on('close', () => {
    console.log('连接断开了')
  })

  // 注册一个error，处理用户的错误信息
  connect.on('error', () => {
    console.log('用户连接异常')
  })
})

server.listen(PORT, () => {
  console.log('websocket服务启动成功了，监听了端口' + PORT)
})
```

## 使用socket.io插件

