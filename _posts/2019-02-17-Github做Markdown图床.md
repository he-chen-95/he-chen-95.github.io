---
layout:     post
title:      Github做Markdown图床
subtitle:   Github-Raw文件
date:       2019-02-17
author:     何晨
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - 技术
---

#### github图床

##### 思路：新建仓库，将图片上传到github上，配合[RawGit](https://rawgit.com/)获取图片中的链接。

* 在github上新建repository
* 下载windows版的github (当然也可以直接在github网页上进行上传图片)
* 将需要上传的图片放到本地目录下，比如dandelion.jpeg
* 利用github的windows客户端commit
* 最后push origin

网页浏览复制图片URL，如https://github.com/he-chen/he-chen.github.io/blob/master/img/2016/dandelion.jpeg

将URL中blob替换为raw，即https://github.com/he-chen/he-chen.github.io/raw/master/img/2016/dandelion.jpeg

![github-windows桌面版](https://github.com/he-chen/he-chen.github.io/raw/master/img/2019/win-github-desktop.jpg)

#### GitHub的raw功能

##### 列出所有文件
仓库 URL + find/分支名称，例如：https://github.com/onestark/learn-css/find/master

##### Raw文件
在浏览器中以 text/plain 查看原始文件。

例如，GitHub 文件原链接：https://github.com/he-chen/he-chen.github.io/blob/master/README.md
                       
可通过以下几种 URL 查看 raw 文件：

* https://raw.githubusercontent.com/he-chen/he-chen.github.io/master/README.md
* https://github.com/he-chen/he-chen.github.io/raw/master/README.md
* https://github.com/he-chen/he-chen.github.io/blob/master/README.md?raw=true

##### 文件下载
不支持 Raw 查看的文件，在浏览器中输入或点击上述查看 raw 文件的 URL 时，会对文件进行下载。因此可以通过这个特性，在 GitHub 上直接提供文件的下载功能。支持 Raw 查看的文件，可在浏览器打开 raw 页面，直接 另存为... 保存即可

