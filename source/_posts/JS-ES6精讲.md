---
title: ES6基础
date: 2021-3-5
categories: [JavaScript]
---

学习视频：[ES6精讲](https://biaoyansu.com/i/65930214353131?rd=https://biaoyansu.com/7.10)

## let
* 不可以重复声明
* 无声明提升
* 块级作用域
## const
* 声明时必须赋值
* 不可以重新赋值
* 无声明提升
* 块级作用域
## 变量的解构赋值
**数组**
```js
var [a, b, c] = [1, 2, 3]
// a:1  b:2  c:3
var [a, b, c] = [1, 2]
// a:1  b:2  c:undefined
var [a, ...c] = [1, 2, 3]
// a:1   c:[2, 3]
var [a, b, c = 5] = [1, 2]
// a:1  b:2  c:5
var [a, , c] = [1, 2, 3];
// a:1  c:3
```
**对象**
```js
var obj = {
  a: 1,
  b: 2
}
let {a: A, b, c = 3 ,d} = obj
console.log(A, b, c, d)
//-> 1, 2, 3, undefined
let {floor, pow} = Math
console.log(floor(1.9), pow(2, 3));
//-> 1, 8
```
<!-- more -->
**其他**
* 获取字符串的长度:`let {length} = 'yo.'`
* 拆解字符串:`let [a, b, c] = 'yo.'`
* 数组形参、对象形参:`function test ([a, b])`

## 字符串方法
* includes  包含子串
* startsWith 以...开头
* endsWith  以...结尾
* repeat(n)  重复n次

## 模板字符串
```js
var title = '野外基地'
var tpl = `
<div>
  <span>${title + `
    <div>${1234}</div>
    `}</span>
</div>`;
```
## Symbol数据类型
```js
let name = Symbol()
{
  var person = {}
  person[name] = 'File1'
  console.log(person[name])
  //-> File1
}
{
  let name = Symbol()
  person[name] = 'File2'
  console.log(person[name])
  //-> File2
}
console.log(person[name]);
//-> File1
```
## proxy
```js
var user = new Proxy({}, {
  get: function (obj, prop) {
    if (prop === 'full_name') {
      return obj.fname + ' ' + obj.lname
    }
  }
})
user.fname = 'Bob'
user.lname = 'Wood'
console.log('user.full_name:', user.full_name);
//-> Bob Wood
```
## set 
去除重复的值，只保留一个
* `var s = new Set([1, 2, 3, 3])`
* size()  长度
* add()  添加
* delete()  删除
* has()   是否拥有
* clear()  清除