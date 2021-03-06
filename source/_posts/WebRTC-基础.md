---
title: WebRTC基础
date: 2021-11-8
tags: [WebRTC]
categories: [通信]
---


## 简介

`WebRTC (Web Real-Time Communications)` 是一项实时通讯技术，它允许网络应用或者站点，在不借助中间媒介的情况下，建立浏览器之间点对点（`Peer-to-Peer`）的连接，实现视频流和（或）音频流或者其他任意数据的传输。`WebRTC`包含的这些标准使用户在无需安装任何插件或者第三方的软件的情况下，创建点对点（`Peer-to-Peer`）的数据分享和电话会议成为可能。

- 第一，通信双方需要先通过服务器交换一些信息
- 第二，完成信息交换后，通信双方将直接进行连接以传输数据



![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/2/27/1692e05b01790921~tplv-t2oaga2asx-watermark.awebp)



- `RTCPeerConnection`：核心对象，每一个连接对象都需要新建该对象
- `SDP`(`Session Description Protocol`，会话描述协议)：包含建立连接的一些必要信息，比如`IP`地址等，`sdp`由`RTCPeerConnection`对象方法创建，我们目前不需要知道该对象中的具体内容，使用黑盒传输即可
- `ICE`(`Interactive Connectivity Establishment`，交互式连接建立技术)：用户之间建立连接的方式，用来选取用户之间最佳的连接方式
<!-- more -->
## WebRTC实现流程



首先发起方获取视频流，如果成功，则新建`RTCPeerConnection`对象，然后创建`offer`，并发送给应答方。

- `addStream`方法将`getUserMedia`方法中获取的流(`stream`)添加到`RTCPeerConnection`对象中，以进行传输
- `onaddStream`事件用来监听通道中新加入的流，通过`e.stream`获取
- `onicecandidate`事件用来寻找合适的`ICE`
- `createOffer()`是`RTCPeerConnection`对象自带的方法，用来创建`offer`，创建成功后调用`setLocalDescription`方法将`localDescription`设置为`offer`，`localDescription`即为我们需要发送给应答方的`sdp`
- `sendOffer`和`sendCandidate`方法是自定义方法，用来将数据发送给服务器

```
// 引入<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>脚本
// 提升浏览器兼容性
var localConnection
var constraints={
    audio:false,
    video:true
}
navigator.mediaDevices.getUserMedia(constraints).then(handleSuccess).catch(handleError)
function handleSuccess(stream) {
  document.getElementById("video").srcObject = stream
  localConnection=new RTCPeerConnection()
  localConnection.addStream(stream)
  localConnection.onaddstream=function(e) {
    console.log('获得应答方的视频流' + e.stream)
  }
  localConnection.onicecandidate=function(event){
    if(event.candidate){
        sendCandidate(event.candidate)
    }
  }
  localConnection.createOffer().then((offer)=>{
    localConnection.setLocalDescription(offer).then(sendOffer)
  })
}
```

同样的，接收方也需要新建一个`RTCPeerConnection`对象

```
var remoteConnection
var constraints={
    audio:false,
    video:true
    }
}
navigator.mediaDevices.getUserMedia(constraints).then(handleSuccess).catch(handleError)
function handleSuccess(stream) {
  document.getElementById("video").srcObject = stream
  remoteConnection=new RTCPeerConnection()
  remoteConnection.addStream(stream)
  remoteConnection.onaddstream=function(e) {
    console.log('获得发起方的视频流' + e.stream)
  }
  remoteConnection.onicecandidate=function(event){
      if(event.candidate){
          sendCandidate(event.candidate)
      }
  }
}

```

当应答方收到发起方发送的`offer`之后，调用`setRemoteDescription`设置`RTCPeerConnection`对象的`remoteDescription`属性，设置成功之后调用`createAnswer`方法，创建`answer`成功之后将其设置为`localDescription`，然后把`answer`发送给服务器

```
let desc=new RTCSessionDescription(sdp)
remoteConnection.setRemoteDescription(desc).then(function() {
    remoteConnection.createAnswer().then((answer)=>{
        remoteConnection.setLocalDescription(answer).then(sendAnswer)
    })
})

```

当发起方收到应答方发送的`answer`之后，将其设置为`remoteDescription`，至此`WebRTC`连接完成。

```
let desc=new RTCSessionDescription(sdp)
localConnection.setRemoteDescription(desc).then(()=>{console.log('Peer Connection Success')})

```

此时虽然`WebRTC`连接已经完成，但是通信双方还不能直接通信，因为发送的`ICE`还没有处理，通信双方还没有确定最优的连接方式。

应答方收到发起方发送的`ICE`数据时，调用`RTCPeerConnection`对象的`addIceCandidate`方法。

```
remoteConnection.addIceCandidate(new RTCIceCandidate(ice))

```

发起方收到应答方发送的`ICE`数据时，同样调用`RTCPeerConnection`对象的`addIceCandidate`方法。

```
localConnection.addIceCandidate(new RTCIceCandidate(ice))

```

至此，一个最简单的`WebRTC`连接已经建立完成。

##  数据通道

`WebRTC`擅长进行数据传输，不仅仅是音频和视频流，还包括我们希望的任何数据类型，相比于复杂的数据交换过程，创建一个数据通道这个主要功能已经在`RTCDataConnection`对象中实现了：

```
var peerConnection = new RTCPeerConnection();
var dataChannel = peerConnection.createDataChannel("label",dataChannelOptions);

```

`WebRTC`会处理好所有的事情，包括浏览器内部层。浏览器通过一系列的事件来通知应用程序，当前数据通道所处的状态。`ondatachannel`事件会通知`RTCPeerConnection`对象，`RTCDataChannel`对象本身在开启、关闭、发生错误或者接收到消息时会触发对应的事件。

```
dataChannel.onerror = function (error){
    console.log(error)
}

dataChannel.onmessage = function (event){
    console.log(event.data)
}

dataChannel.onopen = function (error){
    console.log('data channel opened')
    // 当创建一个数据通道后，你必须等onopen事件触发后才能发送消息
    dataChannel.send('Hello world')
}

dataChannel.onclose = function (error){
    console.log('data channel closed')
}

```

数据通道`datachannel`建立的过程略微不同于建立视频流或音频流双向连接，`offer、answer、ice`处理完毕之后，由一方发起请求即可。

```
localConnection = new RTCPeerConnection();

sendChannel = localConnection.createDataChannel("sendChannel");
sendChannel.onopen = handleSendChannelStatusChange;
sendChannel.onclose = handleSendChannelStatusChange;

```

接收方此时并不需要再次调用`createDataChannel`方法，只需要监听`RTCPeerConnection`实例对象上的`ondatachannel`事件就可以在回调中拿到发送方的请求，数据通道就建立起来了。

```
remoteConnection = new RTCPeerConnection();
remoteConnection.ondatachannel = receiveChannelCallback;

function receiveChannelCallback(event) {
    receiveChannel = event.channel;
    receiveChannel.onmessage = handleReceiveMessage;
    receiveChannel.onopen = handleReceiveChannelStatusChange;
    receiveChannel.onclose = handleReceiveChannelStatusChange;
  }

```

`dataChannelOptions`传入的配置项是可选的，并且是一个普通的`JavaScript`对象，这些配置项可以使应用在`UDP`或者`TCP`的优势之间进行变化。

- `reliable`:设置消息是否进行担保
- `ordered`:设置消息的接受是否需要按照发送时的顺序
- `maxRetransmitTime`:设置消息发送失败时，多久重新发送
- `maxRetransmits`:设置消息发送失败时，最多重发次数
- `protocol`:设置强制使用其他子协议，但当用户代理不支持该协议时会报错
- `negotiated`:设置开发人员是否有责任在两边创建数据通道，还是浏览器自动完成这个步骤
- `id`:设置通道的唯一标识

## 文件共享

目前，数据通道支持如下类型：

- `String`:`JavaScript`基本的字符串
- `Blob(binary large object)`:二进制大对象
- `ArrayBuffer`:确定数组长度的数据类型
- `ArrayBufferView`:基础的数组视图

其中，`Blob`类型是一个可以存储二进制文件的容器，结合`HTML5`相关文件读取`API`，可以实现文件共享的功能。