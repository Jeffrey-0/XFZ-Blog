---
title: Electron基础
date: 2021-10-10
tags: [桌面端, Electron]
categories: [框架]
---

> Electron: 使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序

## HelloWorld

### 项目启动

1. 克隆electron初始项目

   ```bash
   git clone https://github.com/electron/electron-quick-start.git
   ```

2. 安装依赖

   ```bash
   npm i
   ```

3. 项目启动

   ```shell
   npm start
   ```
<!-- more -->
### 启动失败解决

```shell
Electron failed to install correctly, please delete node_modules/electron and try installing
```

1. 删除node_modules文件夹

2. 安装全局yarn 

   ```shell
   npm install yarn -g
   ```

3. 通过yarn安装依赖 `npm install`

   ```shell
   yarn install
   ```

4. 重新启动程序

   ```shell
   yarn start
   ```

   

## bug

### 自定义的js文件中无法访问require

* 报错信息

```shell
错误信息： require is not defined
```

* 解决方案

在main.js文件中new BrowserWindow参数中添加webPreferences属性

```js
const mainWindow = new BrowserWindow({
    webPreferences: {
        // 浏览器的js可以支持node接口
        nodeIntegration: true,
        contextIsolation: false
    }
})
```

### electron-vue项目出现webpack_hmr访问不了

* 报错信息

```shell
GET http://localhost:9080/__webpack_hmr net::ERR_ABORTED
```

* 解决方案

1. 将项目中 .electron-vue/dev-runner.js打开
2. 定义到第二个WebpackDevServer 把 app.use(hotMiddleware)展开，取消注释

### 下载不了资源

####  res.data.pipe is not a function



#### Uncaught (in promise) Error: certificate has expired



### build打包报错

1. tasked修改名称
2. mult安装包
3. 翻墙
4. 不能在中文路径下