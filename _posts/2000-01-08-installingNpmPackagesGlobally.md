---
layout: post
title:  "安装一个可以全局使用的包"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '08'
---

安装 npm 包有两种方式：局部安装或者全局安装。选择用哪一种方式安装取决于你想怎么用这个包。

如果你想要把它作为像 grunt CLI 那样的命令行工具使用的话，那么你需要进行全局安装；另一方面，如果是在自己的模块里，使用 Node 的 require 方法依赖这个包，那么你需要在局部安装。

在全局环境下安装包，只需使用命令 `npm install -g <package>` 即可，例如：

```bash
npm install -g jshint
```

如果出现 EACCES 错误，则需要[修改权限](https://docs.npmjs.com/getting-started/fixing-npm-permissions)。你也可以尝试使用 `sudo` ，但是**应避免这样使用**：

```bash
sudo npm install -g jshint
```
