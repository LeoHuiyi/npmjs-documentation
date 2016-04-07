---
layout: post
title:  "创建 Node.js 模块"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'getting-started'
order: '11'
---
Node.js 模块是一种可以被发布到 npm 上的包。当你创建一个新的模块，你需要从创建一个 package.json 文件开始。

可以使用 `npm init` 来创建 package.json 文件，它会提示你输入 package.json 的名称和版本两个字段。你还需要一个主文件，这个文件默认是 index.js 。

如果你想要添加作者信息字段，可以使用以下格式（ email 和网站都是可选的）：

```bash
Your Name <email@example.com> (http://example.com)
```

一旦创建了你的 package.json 文件，接下来你需要创建你的模块被 required 时要加载的文件。如果你使用的默认设置，这个文件就是 index.js 。

在那个文件中，添加一个函数作为 exports 的属性，这样这个函数就可以被其他代码使用了。

```bash
exports.printMsg = function() {
  console.log("This is a message from the demo package");
}
```

测试：

1. 在 npm 上发布你的包。
2. 在你的项目文件夹外新建一个目录并且跳到那个目录。
3. 执行 `npm install <package>`。
4. 创建一个 test.js 然后 requires 你的包并调用方法。
5. 执行 `node test.js` ，输出信息。
