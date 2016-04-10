---
layout: post
title:  "创建 Node.js 模块"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'getting-started'
order: '11'
---
Node.js 模块是一种可以被发布到 npm 上的包。当你想创建一个新的模块时，你需要从创建一个 package.json 文件开始。

可以使用 `npm init` 来创建 package.json 文件，它会提示你输入 package.json 的名称和版本两个字段。你还需要为 `main` 字段指定一个值（路径），默认是 index.js 。

如果你想要为 `author` 字段添加信息，可以使用以下格式（ email 和网站都是可选的）：

```bash
Your Name <email@example.com> (http://example.com)
```

一旦你的 package.json 文件被成功创建了，你就需要为这个模块创建一个入口文件。如果你使用的默认设置，这个文件就是 index.js 。

在这个文件中，添加一个函数作为 exports 的属性，这样这个函数就可以被其他代码使用了。

```bash
exports.printMsg = function() {
  console.log("This is a message from the demo package");
}
```

测试：

1. 在 npm 上发布你的包。
2. 在你的项目文件夹外新建一个目录并且进入到这个目录。
3. 执行 `npm install <package>`。
4. 创建一个 test.js 文件 然后引入了上面安装的那个包，并执行其中方法的。
5. 执行 `node test.js` ，查看输出信息。
