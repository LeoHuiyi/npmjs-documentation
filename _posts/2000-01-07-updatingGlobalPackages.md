---
layout: post
title:  "更新安装在全局的包文件"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '09'
---
有1个需要替换的连接

使用 `npm install -g <package>` 可以更新全局包文件：

```bash
npm install -g jshint
```

使用 `npm outdated -g --depth=0` 指令则可以找出哪些包需要更新。

使用 `npm update -g` 指令可以更新所有的全局包文件。但是如果 npm 版本低于 2.6.1 的话，推荐使用[这种方法](https://gist.github.com/othiym23/4ac31155da23962afd0e)更新所有过时的全局包文件。
