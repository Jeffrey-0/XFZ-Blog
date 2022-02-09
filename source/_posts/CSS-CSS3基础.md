---
title: CSS3新特性
date: 2021-2-30
categories: [CSS]
---

## 边框&背景

| 属性              | 值（例子）                                   | 描述               |
| ----------------- | -------------------------------------------- | ------------------ |
| border-radius     | 50%                                          | 圆角               |
| box-shadow        | 10px 10px 5px #ccc                           | 盒阴影             |
| background-size   | 100%                                         | 背景图片尺寸       |
| background-origin | content-box、padding-box、border-box         | 背景图片位置       |
| linear-gradient   | linear-gradient(left top,#03a9f4, #f71ab95e) | 渐变：background值 |

## 文本效果&字体

| 属性            | 值（例子）                      | 描述               |
| --------------- | ------------------------------- | ------------------ |
| text-shadow     | 5px 5px 5px #e668a0             | 文本阴影           |
| word-wrap       | break-word                      | 文本强制换行       |
| text-align-last | right                           | 对齐文本的最后一行 |
| text-overflow   | ellipsis                        | 文本溢出时代替     |
| font - family   | "Times New Roman",Georgia,Serif | 字体               |
| font-style      | italic                          | 字体样式           |
| font-weight     | bold                            | 文本粗细           |
<!-- more -->
## 2D转换

| 函数                               | 描述     |
| ---------------------------------- | -------- |
| translate(150px,100px)             | 平移     |
| rotate(150deg)                     | 旋转     |
| scale(1.8,1.8)                     | 放大缩小 |
| skew（20deg,40deg）                | 倾斜     |
| matrix（0.866,0.5,-0.5,0.866,0,0） | 合成功能 |

## 3D转换

**转换属性**

| 属性             | 值   | 描述                   |
| ---------------- | ---- | ---------------------- |
| transform        |      | 应用2D或3D转换         |
| transform-origin |      | 允许改变转换元素的位置 |
| ransform-style   | preserve-3d | 被嵌套元素如何在 3D 空间中显示   |
|  perspective    | 500 | 3D 元素的透视效果   |
| perspective-origin   | 10% 10% |  规定 3D 元素的底部位置    |
| backface-visibility	 | visible |  定义元素在不面对屏幕时是否可见   |

