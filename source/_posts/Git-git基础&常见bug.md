---
title: Git基础&常见bug
date: 2020-11-15
tags: [版本控制]
categories: [Git]
---



基本概念：工作区->暂存区->本地仓库->远程仓库（github）



ping测试 

```shell
 ssh -T -p 443 git@ssh.github.com
```



## 将本地项目发布到github仓库中

* cd进入我们要上传项目的目录（进入该项目）下，可以直接在该项目的文件夹中右键打开Git Base Here

* 在当前项目的目录中生成本地的git管理

  ```shell
  git init
  ```

* 将项目上所有文件添加到仓库中，如果想添加某个特定文件，只需将 . 换成这个特定的文件名即可

  ```shell
  git add .
  ```

* 对这次提交的注释

  ```shell
  git commit -m "first commit"
  ```

* 将本地仓库关联到github中的某个仓库中(已经关联的就不用了)

  ```shell
  git remote add origin https://自己仓库的url地址中
  ```

* 保存操作，将项目上传到github仓库中

  ```shell
  git push -u origin master
  ```
<!-- more -->


## 修改已上传项目中的文件

### 删除远程库的某个文件

* 将远程仓库里面的项目拉下来

* ```shell
  git pull origin master
  ```

* 查看有所有文件夹

* ```shell
  dir
  ```

* 删除这个文件/文件夹（若文件名有空格，用"\\"来拼接）

* ```shell
  git rm -r --cached 文件名
  ```

* 备注

*  ```shell
  git commit -m '备注'
  ```

### 添加文件

* 添加文件

* ```shell
  git add 改好的文件名
  ```

* 备注

* ```shell
  git commit -m '备注'
  ```

* 保存操作

* ```shell
  git push origin master
  ```

## unable to access解决方法

* 删除c盘/用户/用户名中的隐藏文件gitconfig

* 重写添加一个gitconfig

* ```shell
  git config --global user.name "用户名"
  git config --global user.email "邮箱"
  ```

## 传送文件太大解决方法

push项目中报错： RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054

通常是文件太大，第一条测试后无用，第二条测试后可以上传

```shell
$ git config --global http.sslVerify "false"  
```

```shell
git config http.postBuffer 524288000
```

## 回退版本

```shell
git reset --hard HEAD~1
//撤销一次
git push -f
//保存
```

## 玩转git教学

新建文件夹

```shell
$ mkdir '文件夹名'
```

显示当前的绝对路径

```shell
$ pwd
```

新建文件

```shell
$ touch '文件名'
```

修改文件

```shell
$ vi '文件名'
```

## git 提交远程仓库冲突解决

```shell
error: failed to push some refs to 'https://github.com/GDDXZ/RobotDenso.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

### 原因

两人同时fetch了一个分支。 第一个人修改后提交，第二个人提交就失败。

### 解决方法

* 强制推送
$ git push -f
可以提交，会将remote上第一个人的改动冲掉，比较暴力，不太好。

* 正常解决
  先 git fetch origin 然后git merge origin/master, 和本地分支合并, 之后再push

## git push 中提交数据太多

```shell
// 错误
client_loop: send disconnect: Connection reset by peerB/s
fatal: the remote end hung up unexpectedly
fatal: early EOF
fatal: index-pack failed
```

解决办法

当推送大量数据时（初始推送大型存储库，使用非常大的文件进行更改）可能需要 http.postBuffer 在 git 客户端 （而不是服务器）上设置更高的 设置 ；将 Git 缓冲区大小增加到 repo 的最大单个文件大小：

`git config --global http.postBuffer 157286400`

## 强制操作

强制push

`git push origin master -f`

强制pull

```shell
git fetch --all
git reset --hard origin/master
git pull
```

## 更新README.md文件报错

* 错误信息

```
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:Jeffrey-0/XTEH-.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

* 错误原因：由于**github 中的 README.md文件** 不在本地代码目录中

* 解决方法：

1. 这时候可以通过 `git pull --rebase origin master `把**README.md**文件克隆到本地库。
2. 此时再执行 `git push origin master` 就可以完成上传到远程仓库的操作了



## 多人合作下分支操作

1. 新建分支（若有了就跳过）

   ```shell
   git branch 分支名
   ```

2. 切换分支

   ```shell
   git checkout 分支名
   ```

3. 添加所有修改

   ```shell
   git add .
   ```

4. 备注

   ```shell
   git commit -m '备注信息'
   ```

5. 推送内容到远程分支

   ```shell
   git push origin 分支名
   ```

   **合并分支操作**

6. 先切换到master主分支

   ```shell
   git checkout master
   ```

7. 若为多人开发，先将远程master代码先pull

   ```shell
   git pull origin master
   ```

8. 将某分支合并到主分支master上

   ```shell
   git merge 分支名
   ```

9. 推送到远程master

   ```shell
   git push origin master
   ```


## push连接失败报错

报错信息

```
fatal: unable to access ‘https://github.com/***.git/‘: OpenSSL SSL_read: Connection was reset, errno
```

解决办法

```
将 .git/cofig中的url里https链接改成git链接
```

## 无法连接github

1. 找到https://github.com.ipaddress.com/中对应的IP Address
2. 打开：C:\Windows\System32\drivers\etc\hosts
3. 后面加上140.82.113.3 github.com    （此处为对应的IP Address）

## 配置公私钥

1. 生成公钥，配置邮箱(xxx@qq.com 替换成你的邮箱)，一直确定

   ```shell
   $ ssh-keygen -t rsa -b 4096 -C "xxx@qq.com"
   ```

2. 查看公钥

   ```shell
   $ cd ~/.ssh
   $ cat id_rsa.pub
   ```

3. 将公钥拷贝到github中，打开github=>setting=>SSH and GPG keys=> New SSH key

## git add . 出现警告

警告信息

```shell
warning: LF will be replaced by CRLF in ......  
The file will have its original line endings in your working directory
```

原因

```
原因是路径中存在 / 的符号转义问题，false就是不转换符号默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题
```

解决办法

```shell
git config --global core.autocrlf false
```

