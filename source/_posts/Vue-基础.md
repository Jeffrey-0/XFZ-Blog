---
title: Vue基础
date: 2020-12-29
tags: [Vue]
categories: [框架]
---

## 简介

Vue是一个渐进式的框架

* 解耦视图和数据
* 可复用的组件
* 前端路由技术
* 状态管理
* 虚拟DOM

## 安装

* 方式一：直接CDN引入

  ```html
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  
  <!-- 生产环境版本，优化了尺寸和速度 -->
  <script src="https://cdn.jsdelivr.net/npm/vue"></script>
  ```

* 方式二：下载和引入

* 方式三：NPM安装

  ```shell
  $ npm install vue
  ```
<!-- more -->

## 使用

```html
<div id="app">
    <h1>{{ name }}</h1>
    <h1>{{ message }}</h1>
</div>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            name: '小疯子',
            message: 'hello'
        }
    })
</script>
```

## Vue的生命周期

推荐文章：[Vue的生命周期函数钩子](https://baijiahao.baidu.com/s?id=1668393188098846185&wfr=spider&for=pc)

![vue](./vue.png)

## 插值操作

### Mustache语法

```html
<h2>{{ message }}</h2>
```

### v-once

> 只渲染一次，不会随数据的更新而改变

```html
<h2 v-once>{{ message }}</h2>
```

### v-html

> 将string的html解析出来并进行渲染

```html
<h2 v-html="url"></h2>
```

### v-text

> 将string替换文本内容

```html
<h2 v-html="url"></h2>
```

### v-pre

> 不解析，原封不动的显示

```html
<h2 v-pre>{{ message }}</h2>
```

### v-cloak

> 斗篷，在vue解析之前，隐藏元素

```html
<div v-cloak>{{ message }}</div>
```

## 动态绑定属性 v-bind

### 基本使用

> 语法糖   `:`

```html
<img v-bind:src="imgURL">
<a :href="aURL">百度一下</a>
```

### 动态绑定class

* 对象语法
* 数组语法

```html
<div id='app'>
    <h2 :class="json">123</h2>
    <h2 :class="arr">123</h2>
</div>
<script src='../js/vue.js'></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            json: {
                cl: true,
                bg: false
            },
            arr: ['cl', 'bg']
        }
    })
</script>
```

### 动态绑定style

* 对象语法
* 数组语法

```html
<div id='app'>
    <h2 :style="{color: cl, backgroundColor: bg}">123</h2>
    <h2 :style="[style]">123</h2>
    <h2 :style="getStyle()">123</h2>
</div>
<script src='../js/vue.js'></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            cl: 'red',
            bg: 'yellow',
            style: {
                fontSize: '30px',
                color: 'yellow'
            }
        },
        methods: {
            getStyle () {
                return {
                    color: this.cl,
                    backgroundColor: this.bg
                }
            }
        }
    })
</script>
```

## 计算属性computed

**基本使用**

```html
<div id='app'>
    <h2>{{ FullName }}</h2>
</div>
<script src='../js/vue.js'></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            firstName: 'Lee',
            LastName: 'Jeffrey'
        },
        computed: {
            FullName () {
                return this.firstName + ' ' + this.LastName
            }
        }
    })
</script>
```

**与methods的对比**

* methods要带（）

```html
<h1>{{ getFullName() }}</h1>
<h1>{{ fullName }}</h1>
```

* 多次调用时methods运行多次，而computed只运行一次

## 事件监听

### v-on 基本使用

> v-on:事件 = “事件名”
>
> v-on 语法糖 @

```html
<button v-on:click="counter++">+</button>
<button @click="sub">-</button>
```

### 参数问题

* 如果不需要传递其他参数，方法后面可以不加（），默认会将原生事件event参数传递进去
* 如果需要传递参数，同时需要event时，可以通过`$event`作为参数传递
* 参数中的字符串如果不加引号，会在data中寻找是否存在该变量，若不存在，当调用时报错

### v-on修饰符

> 在某些情况下，我们拿到event的目的可能是进行一些时间处理

* .stop： 阻止冒泡，调用event.stopPropagation()
* .prevent: 取消默认行为，调用event.preventDefault()
* .{keyCode | keyAlias}：当事件是从特定键触发时才触发回调
* .native:监听组件根元素的原生事件
* .once 只触发一次回调

## 条件判断 v-if

### v-if基本使用

```html
<h2 v-if="score >= 90">优秀</h2>
<h2 v-else-if="score >= 80">良好</h2>
<h2 v-else-if="score >= 60">及格</h2>
<h2 v-else="score >= 60">不及格</h2>
```

### v-if与v-show的区别

* v-if：当条件为false时，包含v-if指令的元素，根本就不会存在dom中

* v-show：当条件为false 时，通过改变元素的行内样式display：none，v-show元素仍存在

## 循环遍历

> 遍历时，添加`:key`能提高性能，key要具有唯一性，避免用index

**遍历数组**

```html
(item, index)  in  arr
```

**遍历对象**

```html
(value, key, index)  in  obj
```

**数组中响应式的方法**

* push(item) 在尾部添加元素
* pop() 在尾部删除
* shift() 在头部删除
* unshift(item) 在头部添加
* splice(start, length, item) 删除元素、插入元素、替换元素
* sort() 排序
* reverse() 反转

> 注意：通过改变索引改变数组的元素不是响应的

## 高级函数

> 编程范式：命令编程/声明式编程

filter、map、reduce

* filter 过滤

```js
const newNums = nums.filter((i) => i > 100)
```

* map 映射

```js
const newNums2 = nums.map((i) => 2 * i)
```

* reduce 汇总

```js
const newNums3 = nums.reduce((num, i) => num + i)
```

## v-model

双向绑定原理： 给input输入框通过v-bind先进行数据的单向绑定，再通过监听input输入框的输入事件（input）进行数据的改变，实现双向绑定

```html
<div id='app'>
    <input type="text" :value="message" v-on:input="input">
</div>
<script src='../js/vue.js'></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好'
        },
        methods: {
            input (event) {
                // 获取当前事件的元素
                this.message = event.target.value
                console.log(event.target.value)
            }
        }
    })
</script>
```

基本使用

```html
<input type="text" v-model="message">
```

结合使用：radio、checkout、select

**修饰符**

* lazy：当input失去焦点或敲入enter时才更新
* number：强制变成number类型
* trim：去除空格

## 组件化

**组件化和模块化的区别**

* 模块化：是从代码逻辑的角度进行划分；方便代码分层开发，保证每个功能模块的职能单一；
* 组件化：是从UI界面的角度进行划分，前端的组件化，方便UI组件的重用

### 基本使用

1. Vue.extend()创建组件构造器
2. Vue.component()方法注册组件
3. 在Vue实例的作用范围使用组件

```html
<div id='app'>
    <!-- 3.使用组件 -->
    <my-cpn></my-cpn>
    <my-cpn></my-cpn>
</div>
<script src='../js/vue.js'></script>
<script>
    // 1.创建组件构造器对象
    const cpnC = Vue.extend({
        template: `
	<div>
        <h2>标题</h2>
        <p>内容</p>
    </div>`
    })

    // 2.注册组件
    Vue.component('my-cpn', cpnC)

    const app = new Vue({
        el: '#app'
    })
</script>
```

### 全局组件和局部组件

```js
// 1.创建组件构造器对象
const cpnC = Vue.extend({
  template: `
  <div>
    <h2>标题</h2>
    <p>内容</p>
  </div>`
})

// 2.注册组件（全局组件：可以在多个Vue实例下使用）
// Vue.component('my-cpn', cpnC)

const app = new Vue({
  el: '#app',
  // 2.注册局部组件(只能在该Vue实例能用)
  components: {
    myCpn: cpnC
  }
})
```

### 父组件和子组件

```js
// 1.子组件
const cpnC1 = Vue.extend({
  template: `
  <div>
    <h2>标题1</h2>
  </div>`
})
// 2.父组件
const cpnC2 = Vue.extend({
  template: `
  <div>
    <cpn1></cpn1>
    <h2>标题2</h2>
  </div>`,
  components: {
    cpn1: cpnC1
  }
})
```

### 语法糖

```js
// 直接注册组件
// 全局组件语法糖
Vue.component('my-cpn', {
  template: `
  <div>
    <h2>标题</h2>
  </div>`
})
// 局部组件语法糖
const app = new Vue({
  el: '#app',
  components: {
    'cpn2': {
      template:`
      <div>
        <h2>标题2</h2>
      </div>`
    }
  }
})
```

### 分离写法

1. script标签，类型必须为text/x-template

   ```html
   <script type="text/x-template" id="cpn1">
       <div>
         <h2>标题1</h2>
         <p>内容1</p>
       </div>
   </script>
   ```

2. 直接写个template标签，设置id方便关联(推荐写法)

   ```html
   <template id="cpn2">
       <div>
           <h2>标题2</h2>
           <p>内容2</p>
       </div>
   </template>
   ```

### 组件中的数据

```js
Vue.component('my-cpn', {
    template: `
<div>
    <h2>{{ title }}</h2>
    <p>内容</p>
</div>`,
    data () {
        return {
            title: 'abc'
        }
    }
})
```

## 父子组件的通信

![1600864708986](C:\Users\86134\AppData\Roaming\Typora\typora-user-images\1600864708986.png)

**父传子**

在子组件中的props接收父组件传入过来的数据，并在父组件使用子组件时利用v-bind绑定要传输的数据

```html
<!-- 父组件 -->
<div id='app'>
  <cpn v-bind:cmovies='movies' :cmessage='message'></cpn>
</div>

<!-- 子组件 -->
<template id="cpn">
  <div>
    <h2>子组件</h2>
    <h2>{{ cmovies }}</h2>
    <h2>{{ cmessage }}</h2>
  </div>
</template>
<script src='../js/vue.js'></script>
<script>
  const cpn = {
    template: '#cpn',
    data () {
      return {}
    },
    // 父组件传入过来的数据
     props: {
       cmovies: Array,
       cmessage: {
         type: String,   // 类型
         default: 'aaa', // 默认值
         required: true  // 必须传入
       }
     }
  }
  const app = new Vue({
    el: '#app',
    data: {
      movies: [
        '海王',
        '海贼王'
      ],
      message: '消息'
    },
    methods: {
    },
    components: {
      cpn
    }
  })
</script>
```

> 注意：当props中的数据指定类型为对象或数组时，默认值default必须为一个函数



**子传父**

在子组件中通过$.emit向父组件发送事件，在父组件调用子组件中监听子组件的事件

```html
  <!-- 父组件 -->
  <div id='app'>
    <!-- 监听子组件中的item-click事件 -->
    <cpn @item-click="cpnClick"></cpn>
  </div>

  <!-- 子组件 -->
  <template id="cpn">
    <div>
      <h2>子组件</h2>
      <button @click="btnClick(item)" v-for="item in categories" >{{ item.name }}</button>
    </div>
  </template>
  <script src='../js/vue.js'></script>
  <script>
    // 子组件
    const cpn = {
      template: '#cpn',
      data () {
        return {
          categories: [
            {
              id: 'aaa',
              name: '电脑'
            },
            {
              id: 'bbb',
              name: '手机'
            }
          ]
        }
      },
      methods: {
        btnClick(item) {
          // 向父组件发送事件
          this.$emit('item-click', item)
        }
      }
    }
    const app = new Vue({
      el: '#app',
      methods: {
        cpnClick (item) {
          console.log('子组件传过来的数据', item)
        }
      },
      components: {
        cpn
      }
    })
  </script>
```

## BUG

* **vue-cli3 一直运行 /sockjs-node/info?t= 解决方案**

  打开node_modules\sockjs-client\dist\sockjs.js，找到代码1609行，注释掉代码`self.xhr.send(payload)`;

* **Vue项目中，控制台出现`[WDS] Disconnected!`报错**

  打开node_modules\sockjs-client\dist\sockjs.js，找到代码1609行，放掉代码`self.xhr.send(payload)`;的注释

## 查看vue项目中vue和vue-cli的版本号

查看vue-cli的版本号

```shell
vue -V
```

查看vue的版本号

* ```shell
  npm list vue
  ```

* 直接查看package.json中dependencies里面vue的版本号

