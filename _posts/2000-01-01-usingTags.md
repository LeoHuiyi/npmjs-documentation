---
layout: post
title:  "使用标签"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '15'
---

标签是对 [semver](http://semver.org/) (e.g., v0.12) 的一种补充，用来组织和标记不用版本的包。
除了提高了可读性以外，标签还帮助发布者更高效地分他们的包。

<h3 id="adding-tags"><a href="#adding-tags">添加标签</a></h3>

可以使用 `npm dist-tag add <pkg>@<version> [<tag>]`命令为一个指定了版本号的包添加一个标签。查看 [CLI 文档](https://docs.npmjs.com/cli/dist-tag)获取更多信息。

<h3 id="publishing-with-tags"><a href="#publishing-with-tags">发布时添加标签</a></h3>

默认情况下，`npm publish` 将会为你的包添加 `latest` 标签，但如果你使用了 `--tag` 参数，你就可以设定另一个标签了。
下面的例子是当你发布你的包是将为你的包打上 `beta` 标签。

<h3 id="installing-with-tags"><a href="#installing-with-tags">安装时使用标签</a></h3>

像 `npm publish`， `npm install <pkg>` 这样的命令在使用时默认会添加 `latest` 标签，为了覆盖这样的行为，
我们可以使用命令 `npm install <pkg>@<tag>`。下面的例子就会安装标签是 `beta` 版本的 `somepkg` 这样一个包。

``` bash
npm install somepkg@beta
```

<h3 id="caveats"><a href="#caveats">注意事项</a></h3>

由于标签功能与 `semver` 使用的是相同的命名空间，为了避免使用了相同标签名而造成的冲突，最好的解决办法是，
避免使用以数字或者 v 字母开头的标签名。
