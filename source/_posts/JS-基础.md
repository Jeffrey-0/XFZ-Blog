---
title: JavaScript基础
date: 2020-10-15
categories: [JavaScript]
---


## 变量

### 变量的声明和赋值var

```js
var a
a = 15
console.log(a)  //15


b = 17
// 等价于window.b = 25
console.log(b)  //25
```

### 变量的命名规则

* 使用描述性的名称，比如age，sum
* 变量必须以字母、$、_开头，后面可以接数字
* 不推荐用$、_开头，一般为系统默认变量
* 不能使用关键字、保留字
* 区分大小写
<!-- more -->
## 数据类型

* 原始类型

  * 数字：number

    ```js
    // 数据类型
    // 整数、小数、特殊值
    
    // 整数
    // 十进制
    var num = 86
    console.log(num) //86
    
    // 八进制
    var num2 = 070
    console.log(num2) //56
    
    // 十六进制
    var num3 = 0x1f
    console.log(num3)  //31
    
    // 小数,精度有缺陷
    var num_x = 5.01
    console.log(num_x)
    
    // 浮点数的科学计数放
    var num5 = 5.617e7;  //5.617x10^7
    console.log(num5)
    
    // 最大值、最小值
    var num_max = Number.MAX_VALUE
    var num_min = Number.MIN_VALUE
    console.log(num_max, num_min)   //1.7976931348623157e+308  5e-324
    
    // 无穷数
    var num_INF = Number.POSITIVE_INFINITY
    var a = 100
    var a_INF = a.POSITIVE_INFINITY
    console.log(num_INF, a_INF)  //Infinity undefined
    ```

  * 字符串：string

    * length 长度
    * <font color=red> A.contact(B)</font>  拼接 
    * <font color=red>A.indexOf(a,i)</font>  从i位开始查找子串a，返回位置 
    * <font color=red> A.charAt(i) </font>获得第i个字符，从0开始数
    * <font color=red>A.substring(i1,i2)</font> 获取第i1到第i2-1的子串，i2-i1=== length 

  * 布尔：boolean

  * undefined

  * null

* 引用类型

## 比较运算符

* 0 '' {} false null undefined NaN 中==为true的情况

```js
null == undefined 
false == "" 
0 == "" 
0 == false 
```

* 转换规则
  * boolean作为运算数，会把true转成1，false转成0
  * 对象\字符串作为运算数，另一个为数字，试图将对象\字符串转化成数字，失败的话返回NaN，结果为false
  * 俩个字符串比较第一个字符
  * 对象作为运算数，另一个运算数是字符串，试图将对象转换为字符串

## 流程控制

### 分支结构

* if- else
* switch-case

### 循环控制

* while
* do while
* for 
* <font color=red>for-in</font>
* break 跳出循环
* continue 停止当前循环，执行下一次循环

## 数据类型

### 数据类型的判断

* typeof 原始类型

  ```js
  var a = 1
  var b = {name : 'hhh'}
  var c = null
  var d = undefined
  var e = true
  var f = 'hello'
  console.log(a, typeof(a)) // "number" 
  console.log(b, typeof(b)) // "object"
  console.log(c, typeof(c)) // "object"
  console.log(d, typeof(d)) // "undefined"
  console.log(e, typeof(e)) // "boolean"
  console.log(f, typeof(f)) // string
  ```

* instanceof 引用类型

* 判断一个变量是否为数组

  ```js
  A.constructor.name === 'Array'     true
  ```

  

### 转换成数字类型

* Number（）
* parseInt（）
* 俩者区别
  * Number本质上是否能转换成数字，parseInt开头部分看起来像数字
  * Number可以，parseInt不可以：false，null
  * Number不可以，但parseInt可以：数字开头的字符串
  * 都不可以：undefined，字母开头的字符串
* parseFloat()  用于浮点数或科学计数法
* -0 减0 （隐示转换）

### 转换成字符串

* String（）
* A.toString()    可以按进制转换，（）填进制，不填默认10进制
* +''  加空字符串 （隐示转换）

### 转换为boolean类型

* !! 双反 （隐示转换）
* Boolean（） 

### 2进制字符串转换成16进制字符串

```js
// 小练习：二进制转换成16进制
var str = '10101001'
var str1 = parseInt(str,2)
var str2 = str1.toString(16)
console.log(str,str1,str2)
```

## 数组

* 声明

  ```js
  var a = []
  var b = new Array()
  var c = [[1, 2, 3],[1, 2, 3]] 
  ```

* 判断一个元素为数组<font color= red> constructor.name</font>

  ```js
  A.constructor.name === 'Array'
  ```

## 函数

### 标识符（变量，函数名）命名规则

* 小驼峰（变量，函数名）
* 大驼峰（构造函数）
* 匈牙利 类型_小驼峰（避免）

### 函数的声明或定义

* ```js
  //函数的声明
  function fun(){
      return 0
  }
  ```

* ```js
  //函数的表达式，不会污染命名空间
  var fn = function (){
      return 0
  }
  ```

### 立即执行函数

```js
(function () {
    return 1+2
})()
```

## 对象

### 对象的创建

* 字面量

  ```js
  var obj = {}
  ```

* 构造函数

  ```js
  var obj = new Object()
  ```

### 对象属性的增删改查

* 增 

  ```js
  var obj = {}
  obj.a = 'hello'
  obj.b = 100
  // 增，非标识符可以用['']赋值
  obj['1'] = 'Li'
  obj['2'] = function (){
  	console.log(2)
  }
  ```

* 删

  ```js
  // 删
  // 删除某个属性
  delete obj.a
  // 删除整个对象
  obj = null
  ```

* 改

  ```js
  // 改
  obj.b = '123'
  ```

* 查  

  * <mark> in </mark>原型链上的属性也算  
  * <mark>obj.hasOwnProperty() </mark>成员本身的属性
  * <mark>obj.propertyIsEnumerable()</mark>成员本身而且可以枚举的属性 

  ```js
  // 查 
  'a' in obj    -->true
  'toString' in obj   --> true
  obj.hasOwnProperty('a')  -->true
  obj.hasOwnProperty('toString')  -->false
  obj.propertyIsEnumerable('a')  -->true
  obj.propertyIsEnumerable('toString')  -->flse
  ```

* 枚举

  ```js
  // 枚举
  for(var i in obj){
  	console.log(i,obj[i])
  }
  ```

## 函数中的形参和实参（argument对象）

函数在执行之前会将形参和实参进行绑定（一次），改动其一俩者都改变，若参数不够，则不够的参数不会绑定，改动不影响

```js
var fun = function (a, b, c) {
	console.log(a, b, c, fun.length)
	// --> 1, 2, undefined, 3
	console.log(arguments,arguments.length)
	// -->arguments对象
	for (var i in arguments) {
		console.log(arguments[i])
	}
	// --> 1,2
	b = 20
	console.log(b, arguments[1])
	// -->20 20
	arguments[1] = 200
	console.log(b, arguments[1])
	// -->200 200
	c = 30
	console.log(c, arguments[2])
	// -->30 undefined
	arguments[2] = 300
	console.log(c, arguments[2])
	// -->30 300

}

fun(1, 2)
```

## 构造函数

### 构造函数

* 每次以相同的方式来构造对象；如果改变了构造函数，那么所有此后产生的对象都跟着改变
* 特点：大写字母开头

```js
function Person(name, age) {
	// 生成一个对象，this
	this.name = name
	this.age = age
	this.grow = function() {
		this.age ++ 
		return this.age
	}
	// return list指针
}
var LiSi = new Person('LiSi', 23)
```

### 构造函数若有返回值

* 返回值为原始类型（number string boolean）
  * 无new	返回该原始类型
  * 有new    返回this
* 返回值为引用类型（数组，对象，函数）
  * 无论有无new，都返回该引用类型

### 构造函数vs工厂方法

* 函数名
  * 构造函数首字母大写
  * 工厂方法首字母小写
* 调用是构造函数要使用new关键字
* 工厂方法必须有返回值，但构造函数不建议有
* 对对象的引用
  * 构造函数是用this
  * 工厂方法创造谁就用谁

### 包装类

```js
var str = '1234'
console.log(str.concat(56))//-->123456
//上面程序等价于
var str = '1234'
var strTmp = new String(str)
console.log(strTmp.concat(56))
strTmp=null
```

### Date

```js
// Date 日期和时间
console.log(typeof Date);
var time = new Date() 
// 1.当前时间
console.log(time);
// 2.从1970年开始到现在的毫秒数
console.log(time.getTime());
// 3.setFullYear 设定年月日
time.setFullYear(2002, 2, 2)
console.log(time);
// 4.Date()构造函数
var time2 = new Date()
console.log(time2);
// 5.GMT 格林尼治时间 UTC 协调世界时间
console.log(time2.toUTCString());
console.log(time2.toGMTString());
// 6.getFullYear()获取年
console.log(time2.getFullYear());
// 7.getMonth()获取月 + 1 
console.log(time2.getMonth() + 1);
// 8.getDate() 获得日
console.log(time2.getDate());
// 9.getDay()  获得星期
console.log(time2.getDay());
// 10.获得小时、分钟、秒
console.log(time2.getHours());
console.log(time2.getMinutes());
console.log(time2.getSeconds());

// 11.Date格式化
// 	日期格式化
// 	时间格式化
console.log(time2.toLocaleString());
// 2020/4/14 下午4:16:29
console.log(time2.toLocaleDateString());
// 2020/4/14
console.log(time2.toLocaleTimeString());
// 下午4:16:29


// 12.强制转换成毫秒数
var time3 = +new Date()
console.log(time3); //->1586852189336
```



## 内置对象

### Math

* abs	绝对值
* sin、cos、tan  三角函数
* asin、acos、atan、atan2  反三角函数
* 取整
  * round  四舍五入
  * floor  向下取整
  * ceil  向上取整
* fround 最近的单精度数
* exp 指数（e的n次方）
* log  对数 （e为底）
* pow(10,2)   10的2次方
* sqrt  开根号
* max、min 最大值，最小值

### string

* length 长度
* charAt(i)  获取第i位置的字符
* concat(a, b, c)  连接
* indexOf(a)  查询第一个a的位置
* lastIndexOf(a)  查询最后一个a的位置
* replace(a, b) 将第一个a换成b
* replace(/a/g, b) 将所有a换成b
* slice(1, 3)   截取，start end 截取1~2子串
* splite(a) 按a分割字符串，返回一个数组
* substr(1, 3)  截取  start length 截取1~3子串
* substring(1, 3) 截取 start end 截取1~2子串
* toLowerCase()   小写
* toUpperCase() 大写
* trim()   去除俩边空格或缩进

### JSON

JSON 全称 JavaScript Object Notation

* JSON.parse()  将JSON数据转成js对象
* JSON.stringify()  将js对象转成JSON数据

## 定时器

* 定时器，调用时只是把任务放置在队列中，然后返回，等到规定时间到了，会再回来执行该任务（异步）
* setTimeout(fun, 1000)    1000毫秒后执行一次fun
* setInterval(fun, 1000)   每1000毫秒执行一次fun，循环
* clearTimeout() 、clearInterval()   删除定时器

## <font color=red>DOM</font>

DOM--><font color= red>Document Object Model</font>

### DOM能做的三件事

* 操作元素
* 控制元素的样式
* 事件，元素的交互响应

### DOM的使用

* js直接写在html中，不可取
* js与HTML想分离
* js和交互从HTML中剥离

### 获取元素

* document.getElementById()
* document.getElementsByTagName()
* document.getElementsByClassName()
* document.getElementsByName()
  * 只对表单元素有效
* 上面三个获取的是一个集合HTMLCollection，类数组，但不是数组，遍历时避免用for-in ， forEach
* document.querySelector(选择器) 
  * ie7及以下不能使用
* document.querySelectorAll('#demo')
  * for- in无法使用

### DOM的增删替

- 增
  - document.createElement()
  - document.createTextNode()
  - document.createComment()
  - document.createDocumentFragment()
  - parent.appendChild()
  - parent.insertBefore()
- 删
  - parent.removeChild()
  - child.remove()
- 替
  - parent.replaceChild(newChild, originalChild)

## 文本兼容

* innerText 
  * chrome 
  * FF
  * IE8
* textContent
  * chrome
  * FF
  * IE8 不支持
* innerHTML
  * 设置的是HTML原始字符串
  * 可以直接放标签

## 事件

### 事件绑定

1. onType = fun
   * 兼容性非常好,相当于在DOM上的Attribute
   * 如果调用俩次，后面的回调会覆盖前面的回调
2. addEventListener('事件', fun)
   * IE8及以下不兼容
   * 可以重复调用
3. attachEvent('onType', fun)
   * chrome不支持
   * this指向Window
   * IE11及以上不支持

```js
//兼容ie和chrome的添加事件方法
Element.prototype.addEvent = function addEvent( type, func) {
	if (this.addEventListener) {
		this.addEventListener(type, func)
	} else if (this.attachEvent){
		this.attachEvent('on' + type, function (){
			func.call(this)
		})
	} else {
		this['on' + type] = func
	}
}
```

### 事件的解绑定

1. onType = null
2. removeEventListener('事假', funName)
   * 只能删除addEventListener加上去的
   * 函数必须要有函数名或变量名
3. detachEvent(on+'事件' ，funName)

## 原型和原型链

### 原型

* 原型： 让所有的构造函数生成的对象可以共享属性和方法

* 构造函数，对象（实例），构造函数的原型之间的联系

  ```js
  对象 = new 构造函数（）
  对象.__proto__ === 构造函数.prototype ===  原型
  原型.construct === 构造函数 === 对象.__proto__.construct === 构造函数.prototype.construct
  ```

* 例子

  ```js
  function Person2 (name, age, saidWords) {
    this.name = name
    this.age = age
  }
  Person2.prototype.say = function (saidWords) {
    console.log(saidWords)
  }
  var person6 = new Person2('feng', 25, 'world')
  var person7 = new Person2('feng2', 26, 'world2')
  person6.say('world3')
  person7.say('world4')
  console.log(person6.say === person7.say)
  ```

* 判断实例是否属于某构造函数

  ```js
  var obj = new Object()
  obj instanceof Object  //->true
  obj.__proto__.constructor.name  //->Object
  ```

* 实例和构造函数的关系
  * 在构造函数原型上的属性和方法，是共享的
  * 写实例：直接在实例上增加的方法和属性，是属于实例本身的，不会影响构造函数的原型
  * 读实例：首先在实例中寻找该方法或属性，如果找不到上原型上找，如果还是找不到，就返回undefined
  * 删除

### 原型链

* 构造原型链的步骤
  * 从Object开始，没一层底层的构造函数构造出实例，作为上一层构造函数的原型对象
  * 构造好后，通过对象的\_\_proto\_\_,可以一直追溯到Object/null，这个链表称为原型链
* 原型链的性质
  * 所有挂在原型链<mark>对象</mark>的属性和方法，能够被所有派生实例共享
  * 如果访问一份实例的属性或方法，会从对象本身找起，如果没有，则沿着原型链由近至远寻找，如果找不到返回undefined

## 正则表达式

* 正则表达式的定义
  * 正则表达式允许程序员定义一系列的规则，这种规则称为模式（pattern) ,并且可以检测输入的字符串是否和这种模式相匹配
  * 底层是有限自动状态机

* 表达式，参数
  * [0-9] :匹配从0-9其中的任意一个数字
  * \+ : 量词，必须出现至少一次，1次或多次
  * [^] :排除

* 例子

  ```js
  // 正则表达式
  var str1 = '1232a91234'
  var str2 = '123123912314'
  
  // 1.正则表达式类
  var regExp = new RegExp('[0-9]+', 'g')
  // var regExp = /[0-9]+/g
  console.log(str1.match(regExp))
  // ->["1232", "91234"]
  console.log(regExp.test(str1))
  // ->true
  console.log(regExp.test(str2))
  // ->true
  
  // 2.直接量，直接表示正则表达式 /表达式/参数
  console.log(str1.match(/[0-9]+/g))
  // ->["1232", "91234"]
  console.log(str1.match(/\d+/g))
  // ->["1232", "91234"]
  console.log(str1.match(/[123]/g))
  // ->["1", "2", "3", "2", "1", "2", "3"]
  console.log(str2.match(/123/g))
  // ->["123", "123", "123"]
  console.log(str2.match(/(123)+/g))
  // ->["123123", "123"]
  ```

* 通配符,预定义类
  * \d = [0-9]  数字
  * \D = \[^0-9] 非数字
  * \w = [a-zA-Z_0-9] 数字字母下划线
         变量名、标识符 \[a-zA-Z_]\w*\
  * \w = \[^a-zA-Z_0-9] 其他
  * \s = [\t\n\r\f\v ] 所有的空格或空白
  * \b = 表示边界(俩个字符中间的位置) 一边是\w,一边是\W
  * \B 不是边界，俩边都是\w,或者俩边都是\W
  * ^ 开始
  * $ 结尾

* 练习

  ```js
  // 三个数字组成的门牌号
  /^\d\d\d$/
  // 1楼的门牌号
  /^1\d\d$/
  // 尾号为单号的房间
  /[13579]$/
  // 手机号  例子：11位，130-0000-0000, 13000000000
  /^1[34579]\d-?\d{4}-?\d{4}$/
  // 邮箱：字母，数字，下划线 - . @xxx.xxx.xx 字母，数字，下划线 -
  /^[\w\-\\.]+@[\w\\-]+(?:\.[\w]{2,}){1,3}$/
  ```

  