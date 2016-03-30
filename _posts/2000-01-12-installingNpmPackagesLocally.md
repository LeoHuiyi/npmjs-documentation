---
layout: post
title:  "安装局部的 npm 包"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'getting-started'
order: '04'
---

有3个需要替换的连接

npm 包有两种安装方式：局部安装和全局安装。选择哪种方式取决于你想如何使用它们。

如果你想像使用类似于 Node'js 中 `require` 函数那样依赖自己的模块，那么你可以选择局部安装，
这也是 `npm install` 的默认行为。另一种情况是，如果你想使用命令行工具，如 grunt CLI，
那么你可以[全局安装](https://docs.npmjs.com/getting-started/installing-npm-packages-globally)它。

想要了解更多关于 `install` 命令的行为，请到[CLI 页面](https://docs.npmjs.com/cli/install)查看

<h3 id="installing"><a href="#installing">安装</a></h3>

使用命令下载一个包


```bash
npm install <package_name>
```

这条命令首先会在当前路径下新建一个 `node_modules` 目录（如果这个目录不存在的话），然后会把包下载到这个目录中。

<a href="#test" id="test">测试</a>

为了确认 `npm install` 是否工作正常，请查看 `node_modules` 目录是否存在和它是否已经包含了你刚刚安装的包。
你可以在类 Unix 系统如：“OS X”, “Debian” 中使用 `ls node_modules` 命令查看。如果是 Windows 系统请使用命令 `dir node_modules`

<a href="#example" id="example">例子</a>

我们来安装一个名为 `lodash` 的包，然后看看 `node_modules` 目录的列表内是否能成功展示出来一个名为 `lodash` 的目录。

```bash

npm install lodash
ls node_modules      # Windows 系统使用 `dir node_modules`

#=> lodash
```

<h3 id="which-version-of-the-package-is-installed"><a href="#which-version-of-the-package-is-installed">我们安装了哪个版本的包？</a></h3>

如果项目文件夹中没有 `package.json` 文件，那么默认会安装最新的版本。

但如果存在 `package.json` 文件，将会按照[语义规则](https://docs.npmjs.com/getting-started/semantic-versioning)安装与 package.json 文件中声明的包的版本号范围兼容的最新版本。

<h3 id="using-the-installed-package"><a href="#using-the-installed-package">使用安装了的包</a></h3>

如果包已经在 `node_modules` 中，那么你就可以在你的代码中使用它了。例如，如果你创建了一个 Node.js 模块，那么你就可以 `require` 它了。

<a href="#example1" id="example1">例子</a>

创建一个名为 index.js 的文件，添加如下代码：

``` javascript
// index.js
var lodash = require('lodash');

var output = lodash.without([1, 2, 3], 1);
console.log(output);
```

在终端中执行 `node index.js`。 它将会输出 `[2, 3]`

假如你还没有正确地安装 `lodash`，你将会收到报错：

``` bash
module.js:340
    throw err;
          ^
Error: Cannot find module 'lodash'
# 不能找到 `lodash` 模块
```

解决这个问题的方法，在 `index.js` 所在的目录中执行 `npm install lodash`
