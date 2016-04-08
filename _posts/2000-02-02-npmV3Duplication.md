---
layout: post
title:  "npm3 复制和重复数据删除"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'how-npm-works'
order: '04'
---

让我们继续之前的例子，目前，我们拥有一个依赖了两个模块的应用:

- A 模块, 依赖 v1.0 版本的 B 模块
- C 模块, 依赖 v2.0 版本的 B 模块

![](https://docs.npmjs.com/images/appsofar.png)

那么现在我们考虑一个这样的问题，当我们再次安装一个依赖 1.0版本或2.0版本的 B 的模块将会发生什么？

<h3 id="example"><a href="#example">例子</a></h3>

好，那我们就来实践一下，依赖另一个模块，D 模块。D 模块依赖 v2.0 的 B 模块 。就像 C 模块一样。

![](https://docs.npmjs.com/images/npm3deps5.png)

因为 1.0 版本的 B 模块已经是在目录的第一级，我们便不能将 2.0版本的 B 模块安装在目录的第一级中。因此同样会在 D 模块中嵌套安装 2.0 版本的 B 模块，尽管我们已经在 C 模块下安装了 v2.0 B 模块的一个副本。

![](https://docs.npmjs.com/images/npm3deps6.png)

如果一个二级依赖被载入了两次，但是在目录层次中它并不处于第一层，那么它就会被复制并嵌套在主依赖下。

但是如果一个二级依赖被载入了两次，但是在目录结构中它是安装在第一层的，那他就不会被复制并嵌套在主依赖下。

举个例子，如我们上面所想，我们再来依赖一个 E 模块，像 A 模块一样依赖 1.0 版本的 B 模块。

![](https://docs.npmjs.com/images/npm3deps7.png)

由于 1.0 版本的 B 模块已经安装在了目录的第一级，所以我们不需要复制和嵌套它。我们只需要简单地安装 E 模块并与 A 模块共享 1.0 版本的 B 模块就好了。

![](https://docs.npmjs.com/images/npm3deps8.png)

在终端里会显示成这样：

![](https://docs.npmjs.com/images/tree2.png)

现在 -- 我们要将 A 模块升级到 2.0 版。它依赖 2.0 版的 B 模块，而不是之前的 1.0 版的 B 模块, 看看将会发生什么。

![](https://docs.npmjs.com/images/npm3deps9.png)

**关键是要记住安装顺序的问题**

尽管 A（1.0 版） 是通过我们的 `package.json` 文件安装的第一个模块（安装顺序是根据字母顺序决定的），但是使用交互界面的
`npm install` 命令安装就意味着，2.0 的模块 A 将作为最后一个包被安装。

因此，npm3 在我们执行了 `npm install mod-a@2 --save` 之后会做以下的事情：

- 删除 v1.0 的 A 模块
- 安装 v2.0 的 A 模块
- 它保留了 v1.0 的 B 模块，因为还有 E 模块依赖它
- 将 v2.0 的 B 模块嵌套安装在 v2.0 A模块内，这是因为 v1.0 的 B 模块已经占据了目录的第一级

![](https://docs.npmjs.com/images/npm3deps10.png)

在终端里，大致会显示成如此：

![](https://docs.npmjs.com/images/tree4.png)

现在这种情况显然并不是很理想，我们几乎在每个目录下都有 2.0 版的 B 模块，为了解决重复问题，我们可以执行：

``` bash
npm dedupe
```
这个命令会将所有包中依赖的 v2.0 的 B 模块重定向到目录第一级中被复制出的 2.0 的 B 模块上并删除所有嵌套的复制品。

![](https://docs.npmjs.com/images/npm3deps13.png)

在终端里，大致会显示成如此：

![](https://docs.npmjs.com/images/tree5.png)
