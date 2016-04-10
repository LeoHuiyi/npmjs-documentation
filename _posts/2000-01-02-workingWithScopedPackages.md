---
layout: post
title:  "使用被限定范围的包"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '14'
---

范围限定就想 npm 模块的命名空间一样，如果你的包是以 `@` 开头的，那么它就是一个被限定了使用范围的包。
范围就是 `@` 和斜线之间的所有东西。

``` bash
@scope/project-name
```

每个 npm 用户都有他们自己的使用范围。

``` bash
@username/project-name
```

你可以从[CLI 文档](https://docs.npmjs.com/misc/scope#publishing-public-scoped-packages-to-the-public-npm-registry)中找到更多更深入的信息。

<h3 id="update-npm-and-login"><a href="#update-npm-and-login">升级 npm 并登录</a></h3>

你需要使用 2.7.0 以上的版本 npm，并且在你第一次使用有使用范围的模块时，你需要命令行重新登录 npm。

``` bash
sudo npm install -g npm
npm login
```

<h3 id="initializing-a-scoped-package"><a href="#initializing-a-scoped-package">初始化一个限定范围的包</a></h3>

为了创建这样一个包，你只需要在你包的名字之前加上你的限定范围。

``` json
{
  "name": "@username/project-name"
}
```

如果你使用 `npm init` 命令, 你可以将限定范围设置为 `--scoped` 参数的值。

``` bash
npm init --scope=username
```

如果你一直在使用相同的限定范围的话，你很可能希望将这些设置写进你的[.npmrc](https://docs.npmjs.com/files/npmrc) 文件中。
file.

``` bash
npm config set scope username
```

<h3 id="publishing-a-scoped-package"><a href="#publishing-a-scoped-package">发布限定使用范围的包</a></h3>

无论怎样，发布公开的限定范围的包都是免费的，并且不需要付费订阅。为了可以发布这样的包，需要在发布时为其添加 `assess` 参数。这个设置将会为之后的发布自动保留着。

``` bash
npm publish --access=public
```

<h3 id="using-a-scoped-package"><a href="#using-a-scoped-package">使用限定使用范围的包</a></h3>

无论你想在哪里使用这种包，你只需要在它前面包含限定范围就可以了。

In package.json:

``` json
{
  "dependencies": {
    "@username/project-name": "^1.0.0"
  }
}
```

使用命令行：

``` bash
npm install @username/project-name --save
```

声明方式：

``` javascript
var projectName = require("@username/project-name")
```

更多关于局部私有模块的信息，请参考[npmjs.com/private-modules](http://npmjs.com/private-modules)。
