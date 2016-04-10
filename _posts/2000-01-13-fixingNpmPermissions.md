---
layout: post
title:  "修改 npm 的权限"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '03'
---

当你试图安装一个全局包的时候可能会出现一个 `EACCES` 错误，这个错误代表：你对某个路径没有足够的写的权限，
从而不能将你的包或者命令存到这个路径下。

你可以用一下两种方式来解决这个问题：

1. 修改 npm 默认路径的权限级别
2. 修改 npm 的默认路径

当你准备这样做时，请先将你的计算机进行备份。

<h3 id="option1"><a href="#option1">方式 1: 修改 npm 默认路径的权限级别</a></h3>

1. 找到 npm 目录的路径:

``` bash
npm config get prefix
```

在一些系统中，这个路径会在 `/usr/local` 下。

**注意**: 如果显示出来的路径仅仅是 `/usr`, 那么请选择<a href="#option2">方式 2</a>。

2. 将 npm 目录的拥有者改成当前用户（也就是你的用户名）：

``` bash
 sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}
```

这会改变供 npm 使用的子文件夹和一些其他工具的权限(`lib/node_modules`, `bin`, 和 `share`)。

<h3 id="option2"><a href="#option2">方式 2: 修改 npm 的默认路径</a></h3>

很多时候你并不想改变 npm 默认路径的权限(例如：`/usr`) ，因为这可能会带来一些问题，例如你和其他人公用了同一个操作系统。

替代的方法，你可以将 npm 配置到一个不同的公共目录。在下面的例子中，这个目录是在我们用户的根目录（`~`）下的一个隐藏目录。

1. 为全局安装的包/模块创建一个目录:

``` bash
mkdir ~/.npm-global
```

2. 为 npm 配置一个新的默认路径:

``` bash
npm config set prefix '~/.npm-global'
```

3. 打开 `~/.profile` 文件（如果没有此文件则新建一个） ，添加如下面的代码:

``` bash
export PATH=~/.npm-global/bin:$PATH
```

4.返回到命令行, 更新一下系统的变量:

``` bash
source ~/.profile
```

测试一下: 不使用 sudo 下载一个包并安装到全局

``` bash
npm install -g jshint
```
你可以使用合适的环境变量来代替 2-4步的操作（例如：你不想修改`~/.profile`）

``` bash
NPM_CONFIG_PREFIX=~/.npm-global npm install -g jshint
```
