
---
title: jQuery基础
date: 2020-11-05
tags: [jQuery]
categories: [框架]
---

学习视频：[玩转jQuery-表严肃](https://biaoyansu.com/16.2)

## 选择器
* 标签选择器 $(demo)
* id选择器 $(#demo)
* class选择器 $(.demo)
* 属性选择器 $([class='demo'])
* 伪类选择器 $(demo:first)
## 过滤器
* 同级元素 filter(必须有选择器)
* 后辈元素 find(必须有选择器)
* 父元素 parent()
* 先辈元素 parents()
## 操作样式
* 属性
  * css('属性名','属性值')
  * css({属性名: '属性值', 属性名: '属性值'})
* 类名
  * addClass 增加类名
  * removeClass 删除类名
  * hasClass 检查类名
* 显示/隐藏
  * show 显示
  * hide 隐藏
  * fadeOut(n) n毫秒淡出
  * fadeIn(n) n毫秒淡入
  * slideUp(n) n毫秒向上缩隐
  * slideDown(n) n毫秒向下显现

  <!-- more -->
## 操作DOM
* text()  文本
* html()  包含标签、文本
* append() 追加最后一个子元素
* prepend() 追加第一个子元素
* remove() 删除某个元素
## 事件
` Node.on('事件', fun()) `
* click 点击
* dblclick 双击
* mouseenter 鼠标移入
* mouseleave 鼠标移出
## 操作元素属性
* attr(属性, 值)  显现属性
* prop(属性, 值)  隐性DOM属性
* removeAttr(属性)  删除属性
## 表单及输入
* val()  值
* focus() 聚焦
* blur() 不聚焦
* select() 全选
* form.submit() 提交
## Ajax
```js
$.ajax({
  url: ,
  method: 'get',
  success: function (data) {
  },
  error: function (err) {
  }
});
```
* $.get(url, data, callback)
* $.post(url, data, callback, type)
* $.getJSON(url, data, callback)