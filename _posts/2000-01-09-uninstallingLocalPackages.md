---
layout: post
title:  "卸载安装在局部的包"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '07'
---
你可以通过 `npm uninstall <package>` 从你的 node_modules 目录下移除一个包文件，例如：

``` bash
npm uninstall lodash
```

为了解除这个包在 package.json 文件中的依赖，你需要使用 `save` 参数：

``` bash
npm uninstall --save lodash
```
