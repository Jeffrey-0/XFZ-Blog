---
title: Sass基础
date: 2021-4-8
categories: [CSS]
---

学习课程：[Sass和Less开发](https://www.bilibili.com/video/BV15a4y1v7Yv)

## 介绍

> Sass时一款强化CSS的辅助工具,采用Ruby语言编写的一款CSS预处理器，诞生于2007年，是最大的成熟的CSS预处理语言

## 使用

若使用的编辑器是vscode，则只需安装`easy-sass`插件，即可在保存sass或scss文件的同时编译成对应的css文件

## 注释

```scss
/* 这是暴露出去的注释 */
// 这是隐藏的注释
```

## 变量

* 全局变量 + 局部变量
<!-- more -->
```less
// 全局变量
$color: red;
$color: null;
// !default 若变量还没赋值才生效
$color: #fff !default;
body {
  color: $color;
  div {
    // 局部变量
    // !global 将局部转成全局
    $color: pink !global;
    $color: blue;
    color: $color;
  }
}
div {
  color: $color;
}
```

* 多值变量

```scss
$color: red blue black;
body {
  color: nth($color, 1);
  div {
    color: nth($color, 2);
  }
}
```

* 属性名或类名  #{变量}

```scss
$name: "box";
$attranme: "border";
p.#{$name} {
  #{$attranme}: 1px solid red;
}
```

## 运算

* 数字运算： + - * / %
  * `/` 生效条件：加括号、有变量、运算值
  * `-`左右要有空格
* 颜色运算
  * rgb()自动转换成#格式再运算
* 字符串运算
  * 前面有双引号，结果就有双引号
* 布尔运算：and or not
* 数组运算：list function

## 嵌套

* 选择器嵌套
* 属性嵌套

```scss
// 嵌套
header {
  background: red;
  // 属性嵌套
  border: {
    bottom: 1px solid green;
    top: 1px solid black;
  }
  // 选择器嵌套
  nav a {
    color: gray;
    &:hover {
      color: red;
    }
  }
}

// ==> CSS
header {
  background: red;
  border-bottom: 1px solid green;
  border-top: 1px solid black;
}

header nav a {
  color: gray;
}

header nav a:hover {
  color: red;
}
```

## @规则

* @import 导入

* @media 媒体查询

  ```scss
  $viewportsize: (
    'sm': '(max-width: 500px)',
    'md': '(min-width: 501px) and (max-width: 1000px)',
    'lg': '(min-width: 1001px)'
  );
  body {
    @media screen {
      @media(min-width: 0px) {
        background: red;
      }
    }
    @media #{map-get($viewportsize, 'md')} {
      background: blue;
    }
    @media(min-width: 1000px) {
      background: yellow;
    }
  }
  ```

* @extend 基础

  ```scss
  .error {
    background: red;
    border: 1px solid red;
  }
  .error .bg{
    background: url("img/404.png");
  }
  .info {
    font-size: 12px;
  }
  .usererror {
    @extend .error;
    @extend .info;
    border: 1px solid green;
  }
  ```

* @at-root 返回根元素

* @debug

* @warn

* @error

## 控制指令

* @if

  ```scss
  $isshow: 0;
  p {
    @if $isshow == 1 {
      display: block;
    }
    @else {
      display: none;
    }
  }
  ```

* @for

  ```scss
  // to 不包含最后一个
  @for $i from 1 to 3 {
    .item-#{$i} {
      width: 2em * $i;
    }
  }
  // through 包含最后一个
  @for $i from 1 through 3 {
    .item-#{$i} {
      height: 2em * $i;
    }
  }
  ```

* @each

  ```scss
  @each $var in home, user, search {
    .#{$var}-icon {
      background: url('img/#{$var}.png');
    }
  }
  ```

* @while

  ```scss
  $i:4;
  @while $i > 0 {
    .hide-text-#{$i} {
      overflow: hidden;
    }
    $i:$i - 1;
  }
  ```


## 函数

* 字符串函数

  * unquote ：去除首位和末位的引号
  * quote: 添加首位和末位的双引号（若已有单引号，转成双引号，若已有双引号，则不添加）
  * to-upper-case：转成大写
  * to-lower-case：转成小写

* 数字函数

  * percentage() 将一个不带单位的数转成百分比值
  * round() 四舍五入
  * ceil() 向上取整
  * floor() 向下取整
  * abs() 绝对值
  * min($numbers ...) 最小值
  * max($numbers ...) 最大值
  * random() 随机数

* 列表函数

  * lenth($list) 长度
  * nth($list, $n) 返回列表中指定的某个标签值
  * join($list1, $list2, [$separator]) 将俩个列连接一起
  * append($list1, $val, [$separator]) 将某个值放在列表的最后
  * zip($lists...) 将几个列表合成一个多维的列表
  * index($list, $value) 返回一个值在列表的位置

* 颜色函数

  * rgb($red, $green, $blue)
  * rgba($red, $green, $blue, $alpha)
  * red($color) 取出颜色中的红色部分
  * green($color)
  * blue($color)
  * mix($color-1, $color-2, [$weight]) 混合俩种颜色

* HSL函数 (颜色函数)

  > hue色调，saturation饱和度，lightness亮度，H取值范围是0~360的圆心角，SL的取值范围是0~100%

  * hsl($hue, $saturation, $lightness)
  * hsla($hue, $saturation, $lightness, $alpha)
  * hue($color)
  * saturation($color)
  * lightness($color)
  * adjust-hue($color, $degress) 改变颜色的色相值
  * lighten($color, $amount) 提高亮度
  * darken($color, $amount) 降低亮度
  * saturate($color, $amount) 提高饱和度
  * desaturate($color, $amount) 降低饱和度

* Opacity透明度函数

  * alpha($color)  、 opacity($color)  获取颜色透明度值
  * rgba($color, $alpha) 改变透明度
  * opacify($colorr, $amount)  、 fade-in($color, $amount) 使颜色更不透明
  * transparentize($color,$amount)、fade-out($color,$amount) 使颜色更透明

* Introspection函数

  * type-of($value) : 返回一个值的类型
  * unit($number) 返回一个值的单位
  * unitless($number) 判断一个值是否有单位
  * comparable($number-1, $number-2) 判断俩个值是否可以做加减和合并

* 三元条件函数

  * if ($condition, $if-true, $if-false)

* 自定义函数

  * 函数定义
  * 关键字参数
  * 默认参数

  ```scss
  @function body-width ($content: 50, $border: 1) {
    @return $content + $border;
  }
  body {
    width: body-width($border: 100px);
  }
  ```

## Less和Sass比较

不同之处：

* 使用前提：Less在JS上运行，Sass在Ruby上使用
* 变量定义：Sass以$定义变量，Less以@定义变量
* 处理机制：Less通过客户端处理，Sass通过服务端处理，相比较之下前者解析会比后者慢一点
* Less使用较Sass简单，但Sass更加活跃成熟

相同：

* 混入（Mixins）——class中的class
* 参数混入——可以传递参数的class，就像函数一样
* 嵌套规则——Class中嵌套class，减少重复代码
* 运算——CSS中用上数学
* 颜色功能——可以编辑颜色
* 命名空间——分组样式，从而可以被调用
* 作用域——局部修改样式
* JavaScript赋值——在CSS中使用JavaScript表达式赋值

## vue项目中使用sass

1. 安装依赖(要指定版本，最新版本报错)

   ```shell
   npm i sass-loader@7.3.1
   npm i node-sass@4.14.1
   ```

2. 在style中添加lang=’scss‘（此例子用lang="sass"报错）

   ```vue
   <style scoped lang="scss">
   $color: green;
   h1 {
     color: $color;
   }
   </style>
   ```

3. 若依赖下载太卡可使用淘宝镜像cnpm安装依赖

   ```shell
   npm install -g cnpm --registry=https://registry.npm.taobao.org
   ```

   

