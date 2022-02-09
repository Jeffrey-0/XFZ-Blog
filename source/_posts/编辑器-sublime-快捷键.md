---
title: sublime操作指南
date: 2020-06-29
tags: [技巧, 快捷键]
categories: [工具]
---

## 学习视频

https://www.bilibili.com/video/BV1oJ411A73M?p=12

https://www.imooc.com/learn/40

## 编辑快捷键

|      快捷键      |            操作            |
| :--------------: | :------------------------: |
|      CTRL+L      |          选中整行          |
|     CTRL+KK      |      从光标处删至行尾      |
|   CTRL+SHIFT+K   |          删除整行          |
|   CTRL+SHIFT+D   | 复制光标所在整行，插入行前 |
|      CTRL+J      |           合并行           |
|     CTRL+KU      |          改为大写          |
|     CTRL+KL      |          改为小写          |
|      CTRL+D      |            选词            |
|      CTRL+M      | 光标移动至括号内开始/结束  |
|   CTRL+SHIFT+M   |        选择括号内容        |
|      CTRL+/      |          注释整行          |
|   CTRL+SHIFT+/   |        注释已选内容        |
|      CTRL+Z      |            撤销            |
|      CTRL+Y      |            恢复            |
|      CTRL+M      |     光标跳至对应的括号     |
|      ALT+.       |        闭合当前标签        |
|   CTRL+SHIFT+A   |    选择光标位置父标签对    |
|   CTRL+SHIFT+[   |          折叠代码          |
|   CTRL+SHIFT+]   |          展开代码          |
|     CTRL+KT      |          折叠属性          |
|     CTRL+K0      |          展开所有          |
|      CTRL+U      |             软             |
|      CTRL+T      |           词互换           |
|       TAB        |            缩进            |
|    SHIFT+TAB     |          去除缩进          |
|   CTRL+SHIFT+↑   |         与上行互换         |
|   CTRL+SHIFT+↓   |         与下行互换         |
|      CTRL+K      |     从光标处删除至行首     |
|    CTRL+ENTER    |        光标后插入行        |
| CTRL+SHIGT+ENTER |        光标前插入行        |
|     CTRL+F2      |          设置书签          |
|        F2        |         下一个书签         |
|     SHIFT+F2     |         上一个书签         |
<!--more -->
## 菜单快捷键

|    快捷键    |            操作            |
| :----------: | :------------------------: |
|    CTRL+F    |            查找            |
|   CTRL+KB    |      显示/隐藏侧边栏       |
|    CTRL+F    | 转到（文件名/@标签或函数） |
| CTRL+SHIFT+P |          工具菜单          |
|    CTRL+H    |            替换            |
|    CTRL+P    |          跳转菜单          |
|   CTRL+Tab   |          切换文件          |

## 其他快捷键

| 快捷键               | 操作              |
| -------------------- | ----------------- |
| CTRL+K -> CTRL+D     | 跳过选取          |
| CTRL+D -> ALT+F3     | 全选匹配内容      |
| CTRL+A->CTRL+SHIFT+L | 多行游标          |
| SHIFT+ 鼠标右键移动  | 多行游标          |
| SHIFT+F11            | 专注模式          |
| ALT+SHIFT+数字       | 分屏              |
| ALT+-/ALT+SHIFT+-    | 返回/前进编辑位置 |
| CTRL+G               | 跳转到第N行       |
| CTRL+SHIFT+M         | 选中括号内容      |

## 命令模式

在工具菜单`CTRL+SHIFT+P`下的操作

| 输入                        | 操作                   |
| --------------------------- | ---------------------- |
| ss/set syntax + html/js/... | 语法模式               |
| minimap                     | 打开/关闭小地图        |
| snippects                   | 输入模板（函数、if...) |

## PackageControl插件安装失败

https://www.cnblogs.com/notemore/p/10354918.html

1. 下载channels.json文件，地址：https://pan.baidu.com/s/13KvDl96Hkg588IXh-TxpRA，下载完成后解压，建议将channel_v3.json文件放置到根目录下，方便下面的操作。

2. 选择Preference(首选项)> Package Settings(插件-用户) > Settings-User，点击 进入

3. 然后添加以下代码。 这里，["E:\\channel_v3.json"]实际就是json文件所在路径，所以你要设置成你json对应文件路径

   ```json
   "channels":
        [
            "E:\\channel_v3.json"
        ]
   ```

4. 打开settings设置文件中已经有代码，在代码后面续行，则需要加上英文逗号分隔每个用户设置。输入完成后，保存，然后重启 Sublime text3 即可

## 插件

### JavaScript & NodeJS Snippets（不符合JavaScript Standard style标准）

| 缩写 | 全写                   |
| ---- | ---------------------- |
| fn   | function () { }        |
| cl   | console.log()          |
| gi   | getElementById         |
| gc   | getElementsByClassName |
| ga   | getAttribute           |
| sa   | setAttribute           |
| fe   | forEach                |
| fi   | for in                 |
| jp   | JSON.parse             |
| js   | JSON.stringify         |
| si   | setInterval            |
| st   | setTimeout             |
| me   | module.exports         |
| re   | require                |

### sublime-standardjs-snippets（手动安装）

符合JSStandardStyle规范的snippets插件

### AdvancedNewFile

在项目中任何位置创建新文件，如果路径不存在，则新建该路径的文件夹

按住`CTRL+ALT+N`可调出新建文窗口

```
css/index.css
//在css文件夹里新建index.css文件，若无css文件夹，则新建一个css文件夹
```

### Emmet

快速补充html+css代码

### Http Requester

不用打开浏览器，在sublime中直接测试网络请求（get/post)

* get请求测试

```js
//  127.0.0.1:5000/login
router.get('/login', function (req, res) {
	res. render('login.html')
})

//选中上面的访问地址127.0.0.1:5000/login，按住快捷键ALT+CTRL+R,即可显示http response结果
```

* post请求测试

```js
/*
	POST 127.0.0.1:5000/login
	Content-type: application/x-www-form-urlencoded
	POST_BODY:
	user_name=000&password=000
 */
router.post('/login', function (req, res) {
	var user = JSON.stringify(req.body);
	user = JSON.parse(user);
	
	login(user.user_name,user.password,function (err, is_has, user) {
	if (err) {
		throw err
	}
	if (is_has === 0) {
		res. render('login.html')
	}	
	else {
		req.session.user = user //保存用户到session
		console.log(req.session.user)
		res.redirect('/index') //重定向到首页
	} 
	})
})

//选中上面注释的地址以及数据（POST ...000），按住快捷键ALT+CTRL+R,即可显示http response结果
```

### DocBlockr

```js
/**
 * [hhh description]
 * @param  {[type]} a [description]
 * @param  {[type]} b [description]
 * @return {[type]}   [description]
 */
function hhh(a, b) {
	
}

//必须在函数的上一行，只需输入/**+enter,即可得以上注释
```

### A File Icon

文件图标

### SideBarTools

左侧文件操作扩展

### SideBarEnhancements

左侧文件操作扩展

### Local History

本地文件版本记录

### SublimeLinter && SublimeLinter-contrib-standard

根据JSStandardStyle标准进行规范提示

## JavaScript Standard style

* 安装

  * ```shell
    $ npm install standard --global
    /* 全局 */
    ```

  * ```shell
    $ npm install standard --save-dev
    /* 指定文件 */
    ```

* 使用

  * ```shell
    /* 检测 */
    $ standard  textName
    ```

  * ```shell
    /* 自动格式化 */
    $ standard textName --fix
    ```

* 忽略文件

  * ```js
  /* eslint-disable */
    ```

* 忽略下一行

  * ```js
    // eslint-disable-next-line
    ```

* 全局声明

  * ```js
    /* global 变量 */
    ```

## snippet中的scope的定义

<mark>新建的snippet应该保存为`.sublime-snippet`文件</mark>

| C++        | source.c++         |
| ---------- | ------------------ |
| CSS        | source.css         |
| HTML       | text.html          |
| JSP        | text.html.jsp      |
| Java       | source.java        |
| JSON       | source.json        |
| Javascript | source.js          |
| Markdown   | text.html.markdown |
| PHP        | source.php         |
| Python     | source.python      |
| SQL        | source.sql         |
| HTML(TCL)  | text.html.tcl      |
| XML        | text.xml           |
| YAML       | source.yaml        |

