---
layout: post
title:  "使用私有模块"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'private-modules'
order: '01'
---

With npm private modules, you can use the npm registry to host your own private code and the npm command line to manage it. This makes it easy to use public modules like Express and Browserify side-by-side with your own private code.

<h3 id="before-we-start"><a href="#before-we-start">开始之前</a></h3>

You need a version of npm greater than 2.7.0, and you'll need to log in to npm again.

``` bash
sudo npm install -g npm
npm login
```

<h3 id="setting-up-your-package"><a href="#setting-up-your-package">Setting up your package</a></h3>

All private packages are scoped.

Scopes are a new feature of npm. If a package's name begins with @, then it is a scoped package. The scope is everything in between the @ and the slash.

``` bash
@scope/project-name
```

When you sign up for private modules as an individual user, your scope is your username.

``` bash
@username/project-name
```

If you use npm init to initialize your packages, you can pass in your scope like this:

``` bash
npm init --scope=<your_scope>
```

If you use the same scope most of the time, you'll probably want to set it in your default configuration instead.

``` bash
npm config set scope <your_scope>
```

<h3 id="publishing-your-package"><a href="#publishing-your-package">发布你的包</a></h3>

操作十分简单

``` bash
npm publish
```

By default, scoped packages are published as private. You can read more about this in the scopes [documentation](/2016/03/29/workingWithScopedPackages.html).

Once it's published, you should see it on the website with a private flag.

<img src="https://docs.npmjs.com/images/private-modules/private-flag.png" style="margin: 0 auto" alt="">

<h3 id="giving-access-to-others"><a href="#giving-access-to-others">赋予其他人权限</a></h3>

If you want to give access to someone, they need to be subscribed to private modules as well. Once they are, you can give them read or read-write access.

You can control access to the package on the access page. To get to the page, click on the Collaborators link or the plus button.

<img src="http://npmblog-images.surge.sh/static-pages/collaborators-page.png" style="margin: 0 auto" alt="">

Add collaborators by entering the username and hitting enter.

<img src="http://npmblog-images.surge.sh/static-pages/add-collaborator.gif" style="margin: 0 auto" alt="">

你也可以通过命令行添加合作者

``` bash
npm owner add <user> <package name>
```

<h3 id="installing-private-modules"><a href="#installing-private-modules">安装私有模块</a></h3>

To install a private module, you must have access to the package. Then you can use install with the scoped package name.

``` bash
npm install @scope/project-name
```

You also use the scoped package name when requiring it.

``` javascript
var project = require('@scope/project-name')
```

<h3 id="switching-from-private-to-public"><a href="#switching-from-private-to-public">将私有模块变为公共模块</a></h3>

你也可以使用命令行来管理权限：

``` bash
npm access restricted <package_name>
```

The package will be removed from listings on the site within a few minutes of making it private.
