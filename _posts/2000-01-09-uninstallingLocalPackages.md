---
layout: post
title:  "卸载安装在局部的包文件"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '07'
---
你可以通过`npm uninstall <package>`从你的node_modules目录下移除一个包文件，例如：
`npm uninstall lodash`

为了解除package.json文件中的依赖，你需要使用`save <变量名>`，例如：
`npm uninstall --save lodash`
