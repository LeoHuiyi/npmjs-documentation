---
layout: post
title:  "发布 npm 包"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '12'
---
你可以发布任意包含 package.json 文件的目录，比如一个 node 模块。

### 创建用户

为了发布你的 npm 包，你需要有一个 npm 注册表的用户。如果没有，用 `npm adduser` 创建一个。如果你在网页上创建，使用 `npm login` 在客户端存储你的凭据。

测试：用 `npm config ls` 来确保你已将凭据存储在客户端。浏览 [https://npmjs.com/~](https://npmjs.com/~) 来确认它已经被添加到注册表。

### 发布 npm 包

用 `npm publish` 发布包。

除了像 npm-developers 中的描述一样在局部 `.gitignore ` 或者 ` .npmignore` 文件被忽略，目录内的所有文件都会被包含进去。

测试：浏览 [https://npmjs.com/package/<package>](https://npmjs.com/package/<package>) ，你应该能看到你新发布的包的信息。

### 更新 npm 包

当你对包内容做了更改，可以使用 `npm version <update_type>` 更新包， update_type 是一种语义版本发布类型，补丁 ，小改动，或者重大更改。这个命令将改变 package.json 中的版本号。注意如果你有一个Git仓库这个操作也会添加一个此版本号的标签。

更新版本号之后，你可以再次执行 `npm publish` 来发布。

测试：浏览 [https://npmjs.com/package/<package>](https://npmjs.com/package/<package>) ，这个包的版本号应该被更新了。

除非你的包发布了新版本，否则显示在网站中的自述文件将不会被更新，所以你需要运行 `npm version patch` 和 `npm publish` 来更新显示在网站上的文档。
