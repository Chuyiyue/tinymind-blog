---
title: API的部署　　
date: 2024-09-19T13:01:16.555Z
---

　　

将api.zip解压至网站根目录

将Api..php上传到Action

## 替换域名

1. 搜索bbsurl，打开main.
2. 找到bbsurl后的域名，复制纯域名(http://bbs.mmmmyun.cn)不带/
3. 全局查找替换域名
### 请使用IP域名

### 全局替换使用vscode，替换后压缩为zip，使用mt文件管理器进行文件的覆盖

## 替换图标

1. 搜索icon.png
2. 删除文件
3. 复制要写入的文件
4. 修改文件名一致

## 首页轮播图

1. 在网站根目录创建
```
huandengpian
```
文件夹

2. 文件夹内五张图片格式为1.png——5.png
 *图片大小要小于1MB，必须为横屏图片* 

## 板块背景图的替换

板块背景图的路径为
```
res/aff8127d8e6.jpg
```
搜索图片名，删除文件，复制要写入的文件，重命名

## 用户称号

在管理后台新建用户组，将需要称号的用户加入用户组

## 文字替换

全局搜索
```
猫爪社区
```
对文字显示代码进行替换，不要替换文件目录代码

## 用户协议

路径为
```
res/xy.html
```
使用html单页修改

## 官方动态

把第一个默认板块名修改为公告，将会自动对接

# 以下不推荐修改

## 官方图标

### 长条

```
res/eb50b178bb7.png
```
### 圆形

```
res/space_forum_official_icon_large.png
```
## 板块置顶

不要修改
不要修改
不要修改

## 登录和注册页面，可修改文字，不建议修改代码




