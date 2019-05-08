---
layout:     post
title:      Markdown 语法指南
subtitle:   语法指南和常见错误
date:       2019-05-03
author:     何晨
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - 技术
---

最近撰写博文，需要用到一些　markdown 语法，下面写一下自己的学习历程。

##### 语法参考

- [Markdown 语法参考](https://github.com/younghz/Markdown)
- [GFM 语法参考](https://github.com/guodongxiaren/README)
- [Packetlife.net Markdown 语法手册](http://packetlife.net/media/library/16/Markdown.pdf)

##### Markdown 转换至其他文件格式

###### Markdown 转换至　PDF 格式

- 可以通过 Chrome 浏览器 打开 .md 文件。选择 '打印'（Ctrl+P），然后更改 '目标打印机' 为 '另存为 PDF'，再进行一些设置后，即可保存为 PDF 文档。- - 也有热心网友提供了优化过的 Markdown2PDF 转换器，[参考地址](http://www.mdtr2pdf.com/index.html)

###### Markdown 转换至　Word 格式

[Pandoc](http://www.pandoc.org/)

- Pandoc 是一个文档格式转换工具。当然，它是用命令行执行的，所以对用户的代码能力有一点点要求。

- 用法：`pandoc -f markdown -t docx -o 内容简介.docx  docs/Introduction.md`

- 其中， -f 为文档来源格式，-t 指定了目标的文档格式，-o 为输出的文档名称， docs/Introduction.md 为待转换的文件。

[Writage](http://www.writage.com/)

- Writage 是一个 Word 插件，只要安装之后，就可以在 Word 中方便地进行文件的相互转换。

##### 常见错误

###### Error 1

错误描述：　本地编辑 .md 文件时 Table 可以完美显示，但是访问 jeklly 博客主页时其无法正确显示

解决方案：　建议在表格前空一行，否则可能影响表格无法显示
