---
title: Less基础
date: 2021-4-5
categories: [CSS]
---

学习课程：[尚硅谷前端less教程](https://www.bilibili.com/video/BV1YW411T7vd)

## less介绍

>less是一种动态样式语言，属于css预处理器的范畴，他扩展了CSS语言，增加了变量、Mixin、函数等特性，是CSS更易维护和扩展，less既可以在客户端运行，也可以借助Node.js在服务端运行。

## 使用

若使用的编辑器是vscode，则只需安装`easy-less`插件，即可在保存less文件的同时编译成对应的css文件

## 注释

```less
/* 这是暴露出去的注释 */
// 这是隐藏的注释
```

## 变量

使用@申明一个变量： @A: B

* 作为普通属性值来使用：直接使用@A

* 作为选择器或属性名： @{A}的形式
<!-- more -->
* 作为URL： @{url}

  ```less
  @color: blue;
  @m: margin-top;
  @selector: #wrap;
  * {
    @{m}: 0;
  }
  @{selector} {
     background: @color;
  }
  ```

* 变量的延迟加载

  ```less
  @var: 0;
  .class {
    @var: 1;
    .brass {
      @var: 2;
      three: @var;
      @var: 3;
    }
    one: @var;
  }
  
  // ==> css
  .class {
    one: 1;
  }
  .class .brass {
    three: 3;
  }
  ```

## 嵌套规则

* 基本嵌套规则
* 平级的使用 &

```less
#wrap {
  .inner {
    &:hover {
    }
  }
}

// ==> CSS
#wrap {
}
#wrap .inner {
}
#wrap .inner:hover {
}
```

## less的混合

> 混合是将一系列属性从一个规则集引入到另一个规则集的方式

* 普通混合
* 不带输出的混合
* 带参数的混合
* 带参数并且有默认值的混合
* 带多个参数的混合
* 命名参数
* 匹配模式
* arguments变量

```less
@selector: #wrap;
// 带多个参数并且有默认值的混合
.center(@w: 100px, @h: 100px, @c:yellow) {
  width: @w;
  height: @h;
  background: @c;
}
@{selector} {
  .inner {
    .center(200px, 200px, pink);
  }
  .inner2 {
     // 命名参数
    .center(@c:black);
  }
}

// ==> CSS
#wrap .inner {
  width: 200px;
  height: 200px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background: pink;
}
#wrap .inner2 {
  width: 100px;
  height: 100px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background: black;
}
```

```less
// file: triangle.less
.triangle(@_, @w, @c) {
  width: 0;
  height: 0;
  border-style: solid;
  overflow: hidden;

}

.triangle (L, @w, @c) {
  border-width: @w;
  border-color: transparent transparent transparent @c;
}

.triangle (R, @w, @c) {
  border-width: @w;
  border-color: transparent @c transparent transparent;
}


// file: 03.less
@import "./triangle.less";
#wrap .sjx {
  .triangle(L, 40px, yellow);
}


// ==> css
#wrap .sjx {
  width: 0;
  height: 0;
  border-style: solid;
  overflow: hidden;
  border-width: 40px;
  border-color: transparent transparent transparent yellow;
}
```

## less运算

在less中可以进行加减乘除的运算,要在其中一个值中添加单位，多个单位取第一个

`width: (100px * 2);`

## less继承

* `.inner:extend(.center){}`
* `.inner {&:extend(.center);}`
* `.inner {&:extend(.center all);}`

## less避免编译

`~" 属性值 "`

## 内置函数

* 字符串函数
  * escape（）通过对特殊字符使用URL编码来对字符串进行编码
  * e() 返回不带引号的字符串
  * %() 格式化一个字符串
  * replace() 替换字符串的文本
* 列表函数
  * length() 将以逗号或空格分割的值列表作为参数
  * extract() 将放回列表中指定位置的值
* 数字函数
* 颜色函数
* 类型函数