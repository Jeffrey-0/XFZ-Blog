---
title: bug-汇总
sticky: 10
password: 317023
abstract: 这是一篇加密文章，请输入密码再查看!
message:  输入密码
---

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
   lsof -i  端口号
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

   

