---
title: HTML知识点
date: 2020-8-29
categories: [HTML]
---


学习视频：[HTML+CSS Web前端开发工程师快速入门必备课程]

## html

* 在新页面进行跳转`traget="_brank"

  ```html
  <a href="https://www.baidu.com" traget="_brank"></a>
  ```

* 有序列表`ol`

* 用于很多文字，`p`段落标签

* input中的type:

  * 单选框radio
  * 多选框checkbox
  * 颜色选择color

* 去除末尾的浮动

  ```html
  <ul class="more">
  	<li><a href="#">空间</a></li>
  	<li><a href="#">百科</a></li>
  	<li><a href="#">hao123</a></li>
  	<li>|</li>
  	<li class="end"><a href="#">更多>></a></li>
  	<div style="clear:both"></div>
  </ul>
  ```
<!-- more -->
## css

* 背景可以多种参数同时设置

  ```css
  background: url()  no-repeat 100% 100% center;
  ```

* font字体属性

   ```css
  font-faimly:
  /* 字体 */
  font-variant: samll-caps;
  /* 小型大写字母 */
  font-weight: bold;
  /* 加粗 */
  ```

* 定位

  ```css
  z-index:2;
  /*需要定位才能用*/
  /*三种定位*/
  position: absolute;
  /*绝对定位，相对于有定位的父元素，如果父元素没有定位，如果父元素没有定位，则相对于html*/
  position: relative;
  /*相对定位，相对于自己，会占用空间*/
  position: fixed;
  /*窗口定位，相对于页面定位*/
  position: inherit;
  /*继承父级*/
  ```

* 元素属性

  ```css
  /*display*/
  display: none;
  /*消失，不占位*/
  display: block;
  /*块状元素，独占一行*/
  display: inline;	
  /*行内元素*/
  display: inline-block;
  /*行内块元素，有块状的属性，但不占一行*/
  ```

* 其他

  ```cs
  /*透明0-1,0全透明，1不透明*/
  opacity: 0;
  
  /*圆角*/
  border-radius: 10px;
  
  /*首行缩进*/
  text-indent: 2px;
  
  /*input中去除点击后的边框*/
  outline: none;
  
  /*去除a连接中的下划线*/
  text-decoration: none;
  
  /*超出显示滑动条*/
  overflow: auto;
  ```

* 选择器

  ```cs
  /*该集合中第一个元素*/
  div:first-child{}
  /*该集合中最后一个元素*/
  div:last-child{}
  ```

## 水平居中解决方案

* 父元素占一整行，子元素属性变成行级元素，父元素设置样式`text-align : center;`
* 元素为块级元素，设置好宽度，设置样式`margin: 0 auto`
* 采用绝对定位

## 元素上下浮动，不在同一行解决方案

* 设置float属性
* 绝对定位

## 图片等比例铺满显示

```html
<!DOCTYPE html>
<html>
<head>
	<title>图片显示</title>
</head>
<style type="text/css">

	div{
		width: 400px;
		height: 400px;
		margin-bottom: 20px;
		background-repeat: no-repeat;
		border: 1px solid #ff0000;
		background-size: cover;
		background-position: center center;

	}
</style>
<body>
	<div style="background-image: url(img1.jpg);"></div>
	<div style="background-image: url(img2.jpg);"></div>
	<div style="background-image: url(img3.jpg);"></div>
	<div style="background-image: url(img4.jpg);"></div>
</body>
</html>
```

## 怪异盒模型box-sizing（css3属性）

```css
box-sizing:border-box;
/*怪异盒模型,padding不会撑大容器，可视区不变，但内容区变小*/
content-box
/*标准盒模型*/
inherit
/*继承父级*/
```

## 浮动

### 各种宽高的计算

* 内容宽（高）= width(height)
* 可视宽（高）= width(height) + padding + border;
* 文档流宽（高） = width(height) + padding + border + margin

### 浮动的特性

1. 块在一排显示
2. 内联支持宽高
3. 默认内容撑开宽度
4. 脱离文档流
5. 提升层级半层
6. margin左右auto失效

### clear特性

1. 只能影响设置该clear的元素有效，不影响整体页面
2. 有局限性

### 解决父级不能包裹浮动子集方法

1. 给父级设置定高，扩展性不好

2. 给父级设置浮动，margin左右失效

3. inline-block,margin左右失效

4. 空标签clear，最小高度问题，产生多余标签

5. br清浮动，不符合结构样式动作三者相分离

6. 使用伪类after（正确）

   ```css
   父级元素:after{
   			content: "";
   			clear: both;
   			display:block;
   		}
   /*ie6/7兼容方法*/
   父级元素{
       zoom:1;}
   ```

### BFC(block formatting context) 标准浏览器

块级格式上下文BFC

BFC触发条件（任意一条）

1. folat的值不为none
2. overflow 的值不为visible
3. display的值为table-cell，table-caption,inline-block中的任何一个
4. position的值不为relative和static
5. width|height|min-width|min-height:(!aotu)  haslayout IE浏览器
6. zoom:(!normal)

BFC能解决的问题

1. 阻止margin的传递
2. 阻止margin的叠加
3. 能够包裹浮动元素

## 弹性盒模型

`display:flex`

1. 排列方向

2. 对齐方向
   

### 容器属性

* flex-direction方向，默认横向排列
  * row	横向
  * row-reverse 反横
  * column 竖向
  * column-reverse反竖向
* flex-wrap是否换行，默认不换行
  * wrap换行
  * wrap-reverse换行反向
* flex-flow 复核型属性，方向+换行
  * colum wrap
  * row nowrap
* justify-content对齐方式（整体）
  * flex-start居左
  * flex-end居右
  * flex-centen居中
  * space-around项目俩侧有剩余空间（平均分配）
  * space-between项目之间有剩余空间（首尾不留白）
* align-item设置主轴的交叉轴属性
  * flex-start向左
  * flex-end向右
  * center居中
  * baseline文字的下划线保持一条水平线
  * stretch拉伸，若项目没有设置高度，则项目的高度等于容器的高度
* align-content 多条交叉轴属性（若容器只有一条交叉轴则不生效）
  * flex-start居左
  * flex-end居右
  * flex-centen居中
  * space-around项目俩侧有剩余空间（平均分配）
  * space-between项目之间有剩余空间（首尾不留白）

### 项目属性

* order排列顺序，默认为0，越小越靠前
* flex按照剩余空间设置项目大小（加上自身）
* flex-grow默认为0，将剩余空间分配（不加上自身）
* flex-shrink:缩小，当一行放不下时，默认1都缩小
* flex-basis伸缩基点，初始比例，和width差不多，设置后会忽略width
* align-self:允许单个项目与其他项目在交叉轴上不一样的对齐方式

## 水平垂直居中方法

* text-align和line-height(只适用于子元素为行级元素)

  ```css
  #box{
  			text-align: center;
  			line-height: 400px;
  		}
  ```

* table（无效）

  ```css
  #box{
      text-align: center;
      display: table;
  }
  #box p{
      display: table-cell;
      vertical-align: middle;
      border: 1px solid #ff0000;
  }
  ```

* table（改动）

  ```css
  #wrap {
        display: table-cell;
        width: 400px;
        height: 400px;
        border: 1px solid #f2f2f2;
        vertical-align: middle;
        text-align: center;
      }
      #wrap .inner {
        width: 200px;
        height: 200px;
        background: pink;
        display: inline-block;
      }
  ```

  

* 定位(普通、calc()、auto)

  ```css
  #box{
  	position: relative;
  }
  #box p{
      position: absolute;
      /*top:50%;
      left: 50%;
      margin-top: -50px;
      margin-left: -50px;*/
      /*left: calc(50% - 50px);
      top: calc(50% - 50px);*/
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      text-align: center;
      line-height: 100px;
  }
  ```

* 弹性盒模型

  ```css
  #box{
  		display: flex;
		justify-content: center;
  		align-items: center;
  }
  ```

## 响应式开发

media

```html
<style type="text/css">
		/*only not and */
		@media (min-width: 1200px){
			div{
				width: 100px;
				height: 100px;
				background-color: red;
			}
		}
	</style>
	<link rel="stylesheet" type="text/css" href="响应式.css" media="(min-width:1200px)">
```

## css3新增的属性和选择器

### 属性选择器

```html
<!DOCTYPE html>
<html>
<head>
	<title>css3新增的样式和选择器</title>
	<style type="text/css">
	/*含有该属性*/
		div[attr]{
			background: #000000;
		}
		/*属性等于*/
		div[attr="div1"]{
			background: #ff0000;
		}
		/*属性中包含某个属性*/
		div[class~="h2"]{
			background: #00ff00;
		}
		/*属性中含有该*/
		div[class*="h"]{
			background: #0000ff;
		}
		/*以..为开头的属性*/
		div[id^="1"]{
			background: #ffff00;
		}
		/*以..为结尾的属性*/
		div[id$="i"]{
			background: #ff00ff;
		}
		/*属性值等于di或者属性以di-开头的值*/
		div[attr|="di"]{
			background: #00ffff;
		}
	</style>
</head>
<body>
	<div id="1ceshi" class="h2 h3" attr="di-v1">测试</div>
</body>
</html>
```

### 结构性选择器

```css
/*选中父元素下面第三个元素，并且该元素是div*/
		div:nth-child(3){
			background: #ff0000;
		}
		/*选中第二个div元素*/
		div:nth-of-type(2){
			background: #00ff00;
		}
		/*选中所有偶数的div*/
		div:nth-of-type(2n){
			background: #000000;
		}
		/*选中最后一个div*/
		div:nth-last-child(1){
			background: #0000ff;
		}
		/*选中空的div*/
		div:empty{
			background: #ffff00;
			width: 20px;
			height: 200px;
		}
		/*第一个并且为div*/
		div:first-child{
			background: #ffffff;
		}
		/*第一个p元素*/
		p:first-of-type{
			background: #ff0000;
		}
		/*父元素中只有一个元素并且为h
		1*/
		h1:only-child{
			background: #ffff00;
		}
		/*父元素中只有一个h1,但可以有其他元素*/
		h1:only-of-type{
			background: #ffff00;
		}
```

### 选择器伪类

```css
/*突出显示活动中的html锚*/
		p:target{
			background: #ff0000;
		}
		/*可点击的控件*/
		input:disabled{
			background: #ffff00;
		}
		/*不可点击的控件*/
		input:enabled{
			background:#00ff00;
		}
		/*已选择的checkbox或radio*/
		input:checked{

		}
		/*该元素的第一行*/
		div:first-line{
			font-size: 22px;
		}
		/*该元素的第一个字符*/
		div:first-letter{
			font-size: 30px;
		}
		/*e元素在用户选中文字时*/
		div::selection{
			background: #00ffff;
		}

```

### 新增样式

```css
		/*文字阴影*/
		div{
			text-shadow: 2px 2px 4px #ff0000;
		}
		div{
			width: 200px;
			height: 400px;
			
		}
			/*省略号,隐藏，不换行*/
		div{
			text-overflow: ellipsis;
			overflow: hidden;
			white-space: nowrap;
		}
		/*背景裁切：背景图片可以在哪里显示*/
		div{
			background-clip: content-box;
		}
		/*元素阴影:水平（必） 垂直（必） 模糊距离 阴影尺寸 阴影颜色 将外部阴影（outset）改为内部阴影（inset）*/
		div{
			box-shadow: 0px 0px 10px 30px #ffaaaa inset;
		}
		/*线性渐变*/
		/*若不设置方向，则不用兼容*/
		div{
			background: linear-gradient(red,yellow);
			background: -webkit-linear-gradient(left,red, yellow,blue);
			background: -webkit-linear-gradient(60deg,red, yellow,blue);
		}
		/*镜像渐变（从中心往外，或从外往内）*/
		/*设置形状的时候（circle,ellipse)，如果该元素是正方形，是无效的*/
		div{
			background: radial-gradient(red, yellow, blue);
			background: radial-gradient(at left bottom,red, yellow, blue);
			background: radial-gradient(ellipse,red, yellow, blue);
		}
```

### 过渡样式

```css
/*过渡：过渡监听，过渡时间，延迟时间，速度*/
/*复合型transition：第一个参数必须为过渡时间，第二个为延迟时间*/
		.demo1{
			width: 100px ;
			height: 100px;
			background: #ff0000;
			/*transition: 2s;*/
			transition-property: all;
			transition-duration: 2s;
			transition-delay: 1s;
			transition-timing-function: 
			linear;
			/*transition: 2s 10s width linear;*/
		}
		.demo1:hover{
			width: 200px;
			opacity: 0.5;
			background: #ffff00;
		}
```

### 2D属性

```css
.frame .in{
			width: 100px;
			height: 100px;
			background: #ffff00;
			transition: 2s;
			/*旋转的基点*/
			transform-origin: top left;
		}
		/*2d属性*/
		.frame:hover .in{
			/*旋转函数*/
			transform:rotate(90deg);
			/*切斜函数*/
			transform:skew(45deg,45deg);
			/*缩放函数，默认是1，可以为负数、正数、小数*/
			transform: scale(0.5);
			/*位移*/
			transform: translate(100px,100px);

		}
```

### 3D属性

```css
/*3d属性*/
		.frame2{
			width: 500px;
			height: 500px;
			border: 1px solid #ff0000;
			display: flex;
			justify-content: center;
			align-items: center;
			/*建立3D模型,视角,透视距离*/
			perspective: 800px;
			/*透视*/
			transform-style: preserve-3d;
			/*观察者的视角，视线消失的位置*/
			perspective-origin: top right right;
		}
		.frame2 .in{
			width: 100px;
			height: 100px;
			border: 1px solid #000000;
			transition: 2s;

		}
		.frame2:hover .in{
			/*旋转*/
			/*transform: rotateY(75deg);*/
			/*transform: rotateZ(75deg);*/
			/*transform: rotate3d(0,1,1,75deg);*/
			/*位移*/
			/*transform: translateZ(400px);
			transform: translate(100px)*/
			/*伸缩,单独使用没有效果*/
		/*	transform: scaleZ(2) translateZ(-100px);*/
			/*和translateZ（-200px）是等价的*/
			transform: scale3d(2,-2,-1) translateZ(-200px);
		}
```

### 动画效果

```css
.div1{
			width: 200px;
			height: 200px;
			background: #ff0000;
			border: 1px solid #000;
			position: absolute;
			left: 50px;
			top: 50px;
			/*必要属性，绑定动画属性*/
			/*函数名，动画时间，延迟时间，匀速，无限次，反向，停止在最后*/
			animation: move 2s 3s linear infinite alternate forwards;
		}
		/*定义动画*/
		@keyframes move{
			/*!from{
				width: 300px;
			}
			to{
				width: 500px;
			}*/
			0%{
				left: 1000px;
				top: 100px;
				background: #ff0000;
			}
			50%{
				left: 300px;
				top: 300px;
				background: #ff0000;
			}
			100%{
				left: 100px;
				top: 200px;
				background: #ff0000;
			}

}
```

## 移动端开发与适配

### 设置视口viewport

```html
<meta name="viewport" content="width=device-width">
```

### 属性

* width (device-width || value)   屏幕分辨率
* user-scalable 是否允许缩放
* initial-scale 初始比例
* minimum-scale 最小缩放比例
* maximum-scale 最大缩放比例
* devicePixelRatio 像素比（即物理像素/css像素，默认是1，设置2可视会变成2倍）

### 移动端默认样式清除

```html
	/*移动端默认样式清除*/
	body{
		font-family: Helvetica;
	}
	body * {
		-webkit-text-size-adjust: 100%;
		/*横竖屏字体变化*/
		-webkit-user-select: none;
		/*去除用户选中*/
	}
	a, input, button{
		-webkit-tap-highlight-color: rgba(0, 0, 0, 0);
		/*按下阴影*/
	}
	input, button {
		border: none;
		-moz-appearance: none;
		-webkit-appearance: none;
		/*解决ios上按钮的圆角问题*/
		border-radius: 0;
		/*解决ios上输入框圆角问题*/
		outline: medium;
		/*去掉鼠标点击的默认黄色边框*/
		background-color: transparent;
	}
```

### 移动端的字体设置

```html
*{
		font-size: 10px;
		font-size: 62.5%;
	}
```



[HTML+CSS Web前端开发工程师快速入门必备课程]:https://ke.qq.com/course/397629?taid=3166095272186173