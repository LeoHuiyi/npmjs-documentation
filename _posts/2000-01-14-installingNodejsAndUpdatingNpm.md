---
layout: post
title:  "安装 nodejs 并更新 npm"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '02'
---

### 安装 Node.js

如果你的系统是 OS X 或者 Windows, 那么安装 Node.js 最好的方式是使用 [nodejs.org](https://nodejs.org/en/) 网站中的安装软件来安装。
如果你使用的是 Linux 系统，你可以使用安装软件，或者你也可以查看是否有更符合你系统版本的 [node 的资源](https://github.com/nodesource/distributions)。

测试: 执行 `node -v`。请确保 node 的版本大于 v0.10.32

### 升级 npm

Node 默认为我们安装了某个版本的 npm。然而 npm 的更新频率比 Node 要高一些。所以请尽量使用最新版本的 npm。

`sudo npm install npm -g`


测试: 执行 `npm -v` 请确保 npm 的版本大于 v2.1.8


### 手动安装 npm

为了更多需求的使用者

npm 模块可以从 https://registry.npmjs.org/npm/-/npm-{版本}.tgz 中下载
