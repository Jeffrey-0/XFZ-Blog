---
title: 展开运算符...
date: 2021-11-7
categories: [JavaScript]
---


## 合并数组

```js
let a = [1, 2, 3]
let b = [4, 5, 6]
let c = [...a, ...b]  // [1, 2, 3, 4, 5, 6]
```

## 浅拷贝对象 & 合并对象

```js
let person1 = {name: 'tom', age: 18, son: {name: 'l'}}
let person2 = {age: 19, sex: '男'}
let person3 = {...person1, ...person2, name: 'jeffrey'}
console.log(person3) // {name: "jeffrey", age: 19, son: {…}, sex: "男"}
```

## 不定个数传参

```js
// 不定个数传参
function sum(...numbers) {
  return numbers.reduce((pre, cur) => pre + cur)
}
sum(1, 2, 3, 4)  // 10
```

## 解构赋值

```js
// 数组
let a = [1, 2, 3, 4, 5]
let [c, ...d] = a
// c: 1       d: [2, 3, 4, 5]

// 对象
let dog = {
  name: 'tom',
  sex: '男',
  age: 2
}
let {name, ...dog1} = dog 
// name: tom       dog1 : {sex: "男", age: 2}
```

## 字符串转成数组

```js
let s = 'jeffrey'
let sArr = [...s]
console.log(sArr) // ["j", "e", "f", "f", "r", "e", "y"]
```



