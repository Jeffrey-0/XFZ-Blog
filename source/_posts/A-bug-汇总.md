---
title: bug-汇总
sticky: 10
password: 317023
abstract: 这是一篇加密文章，请输入密码再查看!
message:  输入密码
---



模板：

**2022-**

***

> 



***



**2022-2-09**

***

> 服务器-xftp上传文件错误？

原因：该文件的操作权限不足, 开放该文件名下所有子文件的读写权限

```
chmod -R 777 文件名
```

***

>  服务器-ubuntu查看端口占用并杀死进程？

1. 查看端口进程

   ```shell
   lsof -i:端口号
   ```

2. 强制杀进程

   ```shell
   kill -9    进程号
   ```

***

> 服务器-端口号开放？

1. 开放端口号
   
   ```shell
   iptables -I INPUT -p tcp --dport 端口号  -j ACCEPT
   ```
   
2. 持久化保存
   
   ```shell
   sudo netfilter-persistent save
   sudo netfilter-persistent reload
   ```

***

<!-- more -->

> 服务器-博客放在443端口，隐藏掉端口号，总是出现偶尔访问不到问题，多刷新几次又可以访问？

未找到解决方案，可能需要备案网站。

***

> 博客-hexo 文章中图片访问路径问题？

1. 将A.png图片放在source/images/路径下
2. 在文章中利用绝对路径  `![img](/images/A.png)`

***



**2022-2-10**

***

> 博客-hexo中加密指定文章？

1. 安装插件

   ```shell
   npm i hexo-blog-encrypt
   ```

2. 修改站点配置文件，启用该插件

   ```yaml
   encrypt:
     enable: true
     default_abstract: 这是一篇加密文章，请输入密码再查看。
     default_message: 输入密码，查看文章。
   ```

3. 在文章的Front-matter区域中添加密码以及显示文本

   ```markdown
   password: 密码
   abstract: 加密文章摘要
   message:  输入框提示
   ```


***



**2022-2-15**

***

> vue中混合机制mixin用法

作用：多个组件可以共享数据和方法，在使用mixin的组件中引入后，mixin中的方法和属性也就并入到该组件中，可以直接使用。钩子函数会两个都被调用，mixin中的钩子首先执行。

1. 定义一个js文件(mixin.js)

   ```js
   export default {
    data() {
     return {
      name: 'mixin'
     }
    },
    created() {
     console.log('mixin...', this.name);
    },
    mounted() {},
    methods: {}
   }
   ```

2. 在vue文件中使用mixin

   ```js
   import mixin from '@/mixin'; // 引入mixin文件
   export default {
    mixins: [mixin]
   }
   ```

***



**2022-2-16**

***

> git查看所有远程分支

```shell
git branch -a
```

***

> 优化vue项目的首屏加载速度，使用打包压缩插件

使用compression-webpack-plugin将打包文件压缩成.gz文件，然后通过nginx的配置，让浏览器直接解析.gz文件。

1. 安装插件,高版本可能会出现报错

   ```shell
   npm i compression-webpack-plugin@5.0.0
   ```

2. 在vue.config.js中配置插件

   ```js
   const compressionWebpackPlugin = require('compression-webpack-plugin')
   
   module.exports = {
     configureWebpack: {
       // 添加插件
       plugins: [
         new compressionWebpackPlugin()
       ]
     }
   }
   ```

3. nginx的服务端中开启gzip压缩配置

   ```json
   server {
       gzip on;
       gzip_static on;
       gzip_min_length 1k;
       gzip_buffers 4 32k;
       gzip_http_version 1.1;
       gzip_comp_level 2;
       gzip_types text/plain application/x-javascript text/css application/xml;
       gzip_vary on;
       gzip_disable "MSIE [1-6].";
   }
   ```

注意：compressionWebpackPlugin()不要配置deleteOriginalAssets: true，否则会出现白屏。

***



**2022-2-17**

***

> git push 的时候报fatal: unable to access 'https://...': Failed to connect to github.com port 443: Timed out

将https改用git

```shell
git remote rm origin
git remote add origin git@github.com:XXX
```

***



**2022-2-23**

***

> js高阶函数reduce用法

记得在函数后面添加一个初始值参数

```js
arr.reduce((total, item) => total + item, 0)
```

***

