---
layout: post
title:  "使用私有模块"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'private-modules'
order: '01'
---

通过使用 `npm` 的私有模块，你可以将你自己的私有代码保存到 `npm` 的注册中心，并可以使用命令行来管理他们。
这会让你的私有代码与公共模块（例如：Express 和 Browserify）一同使用时变得更为方便。

<h3 id="before-we-start"><a href="#before-we-start">开始之前</a></h3>

你的 `npm` 版本需要高于 **2.7.0**，并且你需要登录到 `npm`

``` bash
sudo npm install -g npm
npm login
```

<h3 id="setting-up-your-package"><a href="#setting-up-your-package">设置你的包</a></h3>

有所的私有包都是有使用范围的。

使用范围是 `npm` 的一个新特性。如果一个包的名字以 `@` 开头，那它就是一个有使用范围的包，使用范围就是，`@` 和斜线之间的东西。

``` bash
@scope/project-name
```

当你以个人用户的身份来注册私有模块时，使用范围就是你的用户名。

``` bash
@用户名/project-name
```

如果你使用 `npm init` 来初始化你的包，那你可以像这样传入你的使用范围。

``` bash
npm init --scope=<your_scope>
```

如果你总是用相同的使用范围，你可能会更希望将其设置到你的默认配置中。

``` bash
npm config set scope <your_scope>
```

<h3 id="publishing-your-package"><a href="#publishing-your-package">发布你的包</a></h3>

操作十分简单

``` bash
npm publish
```

默认情况下，限定了使用范围的包会被作为私有包发布，你可以从[使用范围文档](/2016/03/29/workingWithScopedPackages.html)中了解更多。

一旦发布成功，你就需要在网站上使用私有标记来查看它。

<img src="https://docs.npmjs.com/images/private-modules/private-flag.png" style="display: block; margin: 0 auto" alt="">

<h3 id="giving-access-to-others"><a href="#giving-access-to-others">赋予其他人权限</a></h3>

如果你想赋予其他人使用权限，首先他们要订阅私有模块。当他们订阅成功后，你就可以赋予他们只读或者读写的权限了。

你可以在权限页来管理包的使用权限。你可以点击合作者（Collaborators）连接或者加号按钮前往权限页。

<img src="http://npmblog-images.surge.sh/static-pages/collaborators-page.png" style="display: block; margin: 0 auto" alt="">

输入用户名，敲击回车就可添加合作者。

<img src="http://npmblog-images.surge.sh/static-pages/add-collaborator.gif" style="display: block; margin: 0 auto" alt="">

你也可以通过命令行添加合作者

``` bash
npm owner add <user> <package name>
```

<h3 id="installing-private-modules"><a href="#installing-private-modules">安装私有模块</a></h3>

想要安装私有模块，你就需要用使用权限。获得权限之后你就可以使用 `install` 命令来安装了

``` bash
npm install @scope/project-name
```

再引入它时你也需要填写有使用范围的包名。

``` javascript
var project = require('@scope/project-name')
```

<h3 id="switching-from-private-to-public"><a href="#switching-from-private-to-public">将私有模块变为公共模块</a></h3>

你也可以使用命令行来管理权限：

``` bash
npm access restricted <package_name>
```

这个包过几分钟就会从私有的列表中移除。
