---
title: Git常用命令
date: 2021-5-10
tags: [版本控制]
categories: [Git]
---

## 新建代码库

```shell
# 在当前目录新建一个Git代码库
$ git init 

# 下载一个远程项目
$ git clone [url]
```

## 配置

```shell
# 显示当前的git配置
$ git config --list

# 设置提交代码时的用户信息（通常设置全局--global）
$ git config --global user.name "name"
$ git config --global user.email "email address"
```
<!-- more -->
## 增加删除文件

```shell
#  添加指定文件到暂存区
$ git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
$ git add [dir]

# 添加当前目录所有文件到暂存区
$ git add .

# 删除工作区文件，并将这次删除放入暂存区
$ git rm [file1] [file2] ...

# 删除暂存区中的文件，但该文件会保留在工作区
$ git rm --cache [file]

# 改名文件，并放入暂存区
$ git mv [file-original] [file-renamed]
```

## 代码提交

```shell
# 提交暂存区到本地仓库区，message：备注
$ git commit -m [message]

# 使用新的commit，替代上一次提交
$ git commit --amend -m [message]
```

## 分支

```shell
# 列出所有本地分支
$ git branch 

# 列出所有远程分支
$ git branch -r 

# 列出所有本地分支和远程分支
$ git branch -a 

# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

#切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 合并指定分区到当前分区
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]

# 切换分支后直接不能直接git push
$ git push --set-upstream origin [branch-name]
```

## 标签

```shell
# 列出所有tag
$ git tag

# 新建一个tag 在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git tag -d [tag]

# 提交所有tag
$ git push [remote] --tags
```

## 查看信息

```shell
# 显示有变更的文件
$ git status

# 显示当给前分支的版本历史
$ git log

# 显示commit历史
$ git log --stat

# 信息太多，按Q可以退出log
```

## 远程同步

```shell
# 下载远程仓库所有改动
$ git fetch [remote]

# 将本地仓库和远程仓库关联
$ git remote add orign [url]

# 取回远程仓库的变化，并和本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 推送所有分支到远程仓库
$ git push [remote] --all
```

## 撤销

```shell
# 恢复暂存区的指定文件到工作区
$ git checkout -- [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区和工作区，与上次commit保持一致
$ git reset --hard
```

## 版本回退和撤销（重点）

```shell
# 工作区修改，但是未add，想恢复工作区的文件
$ git checkout -- [file]

# 工作区修改，未add，恢复工作区文件
# 工作区修改+add，清空暂存区中某个文件
$ git restore [file]

# 工作区修改+add，未commit，清空暂存区中某个文件
$ git reset HEAD [file] 

# 工作区修改+add，未commit，清空暂存区并还原工作区
$ git reset --hard

# 已经commit或push了
# 先查看日志，看看自己要回到版本几，~1表示回退上个版本,还原三区（本地仓库、缓存区、工作区）
$ git log --pretty=oneline
$ git reset --hard HEAD~1

# 恢复文件后又想回到修改后的文件
$ git reflog
# $ git log --pretty=oneline
$ git reset --hard [commit_id]
```



