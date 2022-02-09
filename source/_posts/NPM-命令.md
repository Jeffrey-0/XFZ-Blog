---
title: NPM常用命令
date: 2021-9-10
tags: npm
categories: [包管理]
---

# npm包管理工具

学习视频：[npm火速上手](https://biaoyansu.com/20.0)

##  常用命令

| 命令         | 功能                  |
| ------------ | --------------------- |
| npm init     | 初始化                |
| npm install  | 安装所有项目依赖      |
| npm help xxx | 查看xxx命令的帮助信息 |

## npm search 搜索 （快捷方式：find, s)

* npm search jquery

## npm install 安装 （快捷方式：i）

* xxx 搜索并安装xxx（局部）。安装多个依赖可用空格隔开
* xxx -g 搜索并安装xxx（全局）
* xxx -D 安装并将依赖信息写入`package.json`中的devDependencies中
* xxx@版本号 指定安装的版本号
<!-- more -->
## npm uninstall 卸载 （快捷方式：rm，r）

* xxx 卸载xxx。多个依赖可用空格分割
* xxx -D 卸载xxx，并将依赖信息从`package.json`中删除

## npm list 列出已安装依赖 （快捷方式： ls）

* 默认列出局部依赖
* `npm list -g`列出已安装的全局依赖

## npm outdated 检查过期依赖

## npm update 更新依赖（快捷方式：up）

* xxx 局部更新xxx
* xxx -g  全局更新xxx

## npm root 查看依赖安装（node_modules)路径

* 默认查看局部安装路径
* -g 查看全局安装路径

## npm view 查看模块的注册信息

* xxx versions 列出xxx 的所有版本
* xxx dependencies 列出xxx的所有依赖