---
layout: post
title:  "npm3 的非确定性"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'how-npm-works'
order: '05'
---

正如我们之前几页例子中所说的那样：

![](https://docs.npmjs.com/images/install-order.png)
（译：你的 `node_modules` 的目录结构和你的依赖树形式取决于**安装顺序**）

如果你，或你的开发团队使用了 `package.json`。就可以使用交互命令 `npm install` 来添加包（就如许多团队使用npm一样），
有一种情况可能会发生：你在本地机器上执行安装后的 `node_modules` 目录会与你同事们的 `node_modules` 目录不太一样，
这种情况也可能会在你的分布、测试和生产服务器上出现。

出现这种情况的原因，简言之是因为，npm3 不是以确定的方式来安装依赖的。

这么解释可能并不能起到安慰的作用，但是在这篇文章中我们会探讨为什么会发生这类事情，以及向你保证它对你的应用不会造成任何影响，
以及展示如何可靠地创建（重建）一个简单，一致的 `node_modules` 目录的步骤。

<h3 id="example"><a href="#example">例子</a></h3>

让我们回到之前用来举例的应用，并倒退几步：

![](https://docs.npmjs.com/images/npm3deps8.png)

这个例子中的，`package.json` 如下：

``` json
{
  "name": "example3",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "mod-a": "^1.0.0",
    "mod-c": "^1.0.0",
    "mod-d": "^1.0.0",
    "mod-e": "^1.0.0"
  }
}
```

在执行了 `npm install` 之后我们可以在终端里看到：

![](https://docs.npmjs.com/images/npm3deps14.png)

现在，我们团队中的某个开发者决定实现一个功能，然后需要将 A 模块升级到 2.0，在 2.0 版本中 A 模块使用 v2.0 的 B 模块取代了之前的 v1.0 的 B 模块。

![](https://docs.npmjs.com/images/npm3deps9.png)

我们的开发者使用交互命令 `npm install` 来安装了新版本的 A 模块，并将其保存到 `package.json` 中：

``` bash
npm install mod-a@2 --save
```

终端会输出

![](https://docs.npmjs.com/images/npm3deps15.png)

现在我们的项目会变成这样：

![](https://docs.npmjs.com/images/npm3deps10.png)

现在开发者实现了这个功能，载入了新版本的 A 模块并将应用推送到了测试服务器，然后我们使用新的 `package.json` 进行安装：

``` json
{
  "name": "example3",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "mod-a": "^2.0.0",
    "mod-c": "^1.0.0",
    "mod-d": "^1.0.0",
    "mod-e": "^1.0.0"
  }
}
```

测试服务器的日志如下：

![](https://docs.npmjs.com/images/npm3deps16.png)

可视化的时候，看起来像这样：

![](https://docs.npmjs.com/images/npm3deps17.png)

发生了什么？！为什么安装完成了之后的结构树与我们开发者本地机器上的结构树不同？

**要记得：最主要的是安装顺序**

当我们的开发者在开发新功能时使用 `npm install` 将 A 模块更新到 2.0 版本时。由于我们的开发者最开始的工作的时候已经执行过 `npm install`,
所以所有列于 `package.json` 中的包已经被安装到了 `node_modules` 文件夹下，在此之后 2.0 版本的模块 A 才被安装。

1.0 版的 B 模块是因为被 1.0 版本的 A 模块依赖才会被添加进目录的第一级，此后由于再次被 1.0 版的 E 模块依赖，才会保留在目录的第一级。
由于 1.0 版的 B 模块存在于目录的第一级，这就导致其他版本的 B 模块就不能在第一级了，所以 2.0 版本的 B 模块就会被嵌套依赖在 v1.0 C 模块和
v1.0 D模块下，并且也成为 v2.0 A 模块的嵌套依赖。

让我们考虑一下测试服务器中会发生什么，项目会推送到一个全新的路径下，此前并不存在一个 `node_modules` 目录。然后执行 `npm install`（这个命令也可能是通过部署的脚本间接执行的）来安装 `package.json` 中的依赖。

`package.json` 中已经含有了 2.0版的 A 模块，并多亏了字母排序（由`npm install` 命令执行的），如今它被第一个安装，而不是最后一个

在一个新建的 `node_nodules` 目录中，当 2.0 版的 A 被首先安装时，它的依赖就会被确定在目录的第一级，因此，2.0 版的 B 模块会被安装到 `node_nodules` 的最顶层。

现在，轮到安装 v1.0 的 E 模块了，它的依赖，也就是 1.0版的 B 模块，由于 2.0 版的存在，便不能占据 `node_nodules` 目录的最顶层了。所以它会被嵌套到 v1.0 的内部。

<h3 id="do-different-dependency-tree-structures-affect-my-app"><a href="#do-different-dependency-tree-structures-affect-my-app">使用不同的依赖结构会不会影响到我们的应用？</a></h3>

完全不会，尽管结构树是不同的，但你的依赖和其他人的依赖却都可以被完整地安装，结构树中的所有的东西都是你需要的，它仅仅在配置上有所不同。

<h3 id="i-want-my-node-modules-directory-to-be-the-same"><a href="#i-want-my-node-modules-directory-to-be-the-same">我希望我的 `node_modules` 目录始终保持一致，该怎么做</a></h3>

`npm install` 命令在用于安装 `package.json` 中描述的依赖时（译：也就是不加参数的时候），将总会生成相同的结构树，这是因为 `package.json` 中的安装顺序始终遵循着字母表。相同的安装顺序便意味着会得到相同的结构树。

你可以在你修改过 `package.json` 之后将你的 `node_modules` 目录删除并重新安装来获得相同的依赖结构树，
