---
title: Bootstrap基础
date: 2020-11-1
tags: Bootstrap
categories: [框架]
---

学习视频[玩转Bootstrap-表严肃]

## 栅格系统

## 按钮 

**样式**

| 类名        | 功能      |
| ----------- | --------- |
| btn         | 声明按钮  |
| btn-default | 默认 灰白 |
| btn-primary | 主要 深蓝 |
| btn-success | 成功 浅绿 |
| btn-danger  | 危险 淡红 |
| btn-info    | 信息 浅蓝 |
| btn-warning | 警告 浅黄 |

**大小**

| 类名   | 功能     |
| ------ | -------- |
| btn-lg | 大       |
| 空     | 默认、中 |
| btn-sm | 小       |
| btn-xm | 超小     |
<!-- more -->

**按钮组**

| 类名               | 功能       |
| ------------------ | ---------- |
| btn-group          | 水平按钮组 |
| btn-group-vertical | 垂直按钮组 |
| btn-toolbar        | 嵌套按钮组 |

## 表单form

```html
  <form class="container">
    <div class="form-group">
      <label class="control-label">用户名</label>
      <input class="form-control" type="text" name="username">
    </div>
<!-- 前置图标 -->
    <div class="input-group">
      <div class="input-group-addon">￥</div>
      <input class="form-control" type="text"></input>
    </div>
  </form>
```

## 导航

| 类名          | 作用       |
| ------------- | ---------- |
| nav           | 声明导航   |
| nav-tabs      | 标签导航   |
| nav-pills     | 胶囊式导航 |
| nav-justified | 平分宽度   |
| nav-stacked   | 竖形       |

## 导航栏

```html
 <div class="container">
    <div class="navbar navbar-default">
    <div class="navbar-header">
      <a href="/" class="navbar-brand">首页</a>
      <a href="/" class="navbar-brand">产品</a>
    </div>
        
    <form class="navbar-form navbar-left">
      <div class="form-group">
        <input type="text" name="" class="form-control">
      </div>
      <button type="submit" name="搜索" class="btn btn-default">搜索</button>
     </form>
        
    <div class="navbar-header navbar-right">
      <a href="" class="navbar-brand">登录</a>
      <a href="" class="navbar-brand">注册</a>
    </div>
  </div>
  </div>
```

## 面板

| 类名          | 作用     |
| ------------- | -------- |
| panel         | 声明面板 |
| panel-default | 默认面板 |
| panel-success | 绿色面板 |
| panel-heading | 面板头部 |
| panel-body    | 面板身体 |
| panel-footer  | 面板底部 |

## 表格

| 类名           | 作用       |
| -------------- | ---------- |
| table          | 声明表格   |
| table-striped  | 黑白相间   |
| table-hover    | 鼠标位变色 |
| table-bordered | 加边框     |

## 分页

| 类名       | 作用     |
| ---------- | -------- |
| pagination | 分页     |
| pager      | 上下页   |
| active     | 当前击中 |
| disabled   | 不可点击 |

## 路径导航

```html
<div class="breadcrumb">
    <li><a href="">首页</a></li>
    <li><a href="">文章</a></li>
    <li class="active"><span >helloworld</span>
</div>
```

## 标签

```html
<p>
  <label class="label label-success">有趣</label> 
  <label class="label label-success">有趣</label> 
  <label class="label label-success">有趣</label> 
</p>
```

## 数字统计(点赞数)

```html
<button class="btn btn-success">
    赞<span class="badge">20</span>
</button>
```

## 弹出框

```html
<div class="alert alert-danger">
        危险
</div>
```

## 列表组

```html
<div class="list-group">
  <a href="" class="list-group-item">123</a>
  <a href="" class="list-group-item">123</a>
</div>
```



[玩转Bootstrap-表严肃]:https://biaoyansu.com/14.1