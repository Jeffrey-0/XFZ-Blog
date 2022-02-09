---
title: HTML5新特性
date: 2021-2-10
tags: [HTML5]
categories: [HTML]
---


## 新元素

**新的语义和结构元素**

| 标签       | 描述                                                 |
| ---------- | ---------------------------------------------------- |
| article    | 页面独立的内容区域                                   |
| aside      | 侧边栏                                               |
| bdi        | 一段文本、使其脱离父元素的文本方向位置               |
| command    | 命令按钮，如单选/复选按钮                            |
| details    | 描述文档                                             |
| dialog     | 对话框                                               |
| summary    | 标签包含details元素的标题                            |
| figure     | 规定独立的流内容（图片、图表、照片、代码等）         |
| figcaption | 定义figure元素的标题                                 |
| footer     | section或document的页脚                              |
| header     | 文档的头部内容                                       |
| mark       | 带有记号的文本                                       |
| meter      | 定义度量衡                                           |
| nav        | 导航链接的部分                                       |
| progress   | 任务的进度                                           |
| ruby       | 定义rudy注释                                         |
| rt         | 字符的解释或发音                                     |
| rp         | 在ruby注释中使用，定义不支持ruby的浏览器所显示的内容 |
| section    | 定义文档中的节                                       |
| time       | 日期或时间                                           |
| wbr        | 文本中何处适合添加换行符                             |
| canvas     | 标签定义图形，比如图表和其他图像                     |
<!-- more -->
**新多媒体元素**

| 标签   | 描述                                 |
| ------ | ------------------------------------ |
| audio  | 音频                                 |
| video  | 视频                                 |
| source | audio、video多媒体资源               |
| embed  | 嵌入的内容，如插件                   |
| track  | 为audio和video的媒介规定外部文本轨道 |

**新表单元素**

| 标签     | 描述                           |
| -------- | ------------------------------ |
| datalist | 与input配合，定义input可能的值 |
| keygen   | 表单的密钥对生成器字段         |
| output   | 定义不同类型的输出             |

**移除的元素**

以下的HTML4.01元素在HTML5已经被删除

| acronym  | applet | basefont |
| -------- | ------ | -------- |
| big      | center | dir      |
| font     | frame  | frameset |
| noframes | strike | tt       |

## 视频-video
| 属性     | 值       | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| width    | px       | 宽度                                                         |
| height   | px       | 高度                                                         |
| src      | url      | 视频地址                                                     |
| controls | controls | 出现控件                                                     |
| autoplay | autoplay | 自动播放，不兼容很多浏览器，可配合muted静音而生效            |
| loop     | loop     | 循环播放                                                     |
| preload  | preload  | 页面加载时进行加载，预备播放，如果有“autoplay",则忽略此属性。 |
| muted    | muted    | 静音                                                         |

```html
 <video  loop muted autoplay src="http://vfx.mtime.cn/Video/2019/03/19/mp4/190319222227698228.mp4" width="600px"  controls="controls"  preload="preload"></video>
```



## 音频-audio

| 属性     | 值       | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| src      | url      | 音频地址                                                     |
| controls | controls | 出现控件                                                     |
| autoplay | autoplay | 自动播放，不兼容很多浏览器                                   |
| loop     | loop     | 循环播放                                                     |
| preload  | preload  | 页面加载时进行加载，预备播放，如果有“autoplay",则忽略此属性。 |

```html
<audio src="李圣杰 - 手放开.mp3"  controls="controls" autoplay="autoplay"></audio>
```

## 拖放

```html
<div id="box" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
  <img draggable="false" src="a.jpg">
  <img id="drag1" draggable="true" src="a.jpg" ondragstart="drag(event)">
  <script type="text/javascript">
function allowDrop (event) {
  event.preventDefault()
  // 取消事件的默认行为
}
// 拖
function drag (event) {
  event.dataTransfer.setData('Text', event.target.id)
}
// 放  
function drop (event) {
  event.preventDefault()
  var data = event.dataTransfer.getData('Text')
  event.target.appendChild(document.getElementById(data))
}
  </script> 
```

## 画布-canvas

```html
<canvas id="myCanvas" width="200px" height="100px"></canvas>
  <script type="text/javascript">
    var demo = document.getElementById('myCanvas')
    var cxt = demo.getContext("2d")
    // HTML5内置对象
    cxt.fillStyle = "pink"
    // 规定颜色
    cxt.fillRect(0, 0, 150, 75)
    // 规定形状，位置，尺寸
    // 从左上角（0， 0）开始绘制150*75的矩形
  </script>
```

## 伸缩矢量图形-内联-svg

```html
  <svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190px">
    <polygon points="100,10 40,180 190,60 10,60 160,180" style="fill:pink;stroke:#444;stroke-width:3;fill-rule:evenodd;" />
  </svg>
```

## 地理定位

```js
// 本地连接无效，需要https：//开头
var x=document.getElementById("demo");
function getLocation()
  {
  if (navigator.geolocation)
    {
  navigator.geolocation.getCurrentPosition(showPosition);
    }
  else{x.innerHTML="该浏览器不支持获取地理位置";}
  }
function showPosition(position)
  {
  x.innerHTML="纬度: " + position.coords.latitude + 
  "<br />经度: " + position.coords.longitude;	
  }
```



## Web存储

* localStorage：没有时间限制的数据存储，关闭浏览器数据仍存在
* sessionStorage：针对一个session的数据存储，关闭浏览器数据消失

## Web Workers

web worker 是运行在后台的JavaScript，不会影响页面性能

```html
<!-- file:Web-Workers.html -->
<script>
var w;
function startWorker() {
    if(typeof(Worker) !== "undefined") {
        if(typeof(w) == "undefined") {
            w = new Worker("demo.js");
        }
        w.onmessage = function(event) {
            document.getElementById("result").innerHTML = event.data;
        };
    } else {
        document.getElementById("result").innerHTML = "抱歉，你的浏览器不支持 Web Workers...";
    }
}
function stopWorker() 
{ 
    w.terminate();
    w = undefined;
}
</script>
```

```js
// file:demo.js
var i = 0
function timedCount () {
  i = i + 1
  postMessage(i)
  setTimeout('timedCount()', 500)
}
timedCount()
```

## 表单

**type输入类型**

| 输入类型     | 描述                 |
| ------------ | -------------------- |
| email        | 邮箱地址             |
| url          | 网址                 |
| number       | 数字类型             |
| range        | 数字的输入域，滑动条 |
| Date pickers | 日期                 |
| search       | 搜索                 |
| color        | 颜色                 |

**属性**

| 属性           | 描述                                 |
| -------------- | ------------------------------------ |
| autocomplete   | from&input属性，自动填充             |
| novalidate     | form属性，不验证                     |
| autofocus      | 获取焦点                             |
| height、width  | 只适用于image类型的input标签         |
| list           | 选项列表                             |
| min、max、step |                                      |
| multiple       | 适用email和file类型的input标签，多值 |
| pattern        | 模式，正则表达式                     |
| placeholder    | 提示                                 |
| required       | 提交时非空                           |

