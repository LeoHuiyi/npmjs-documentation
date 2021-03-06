---
layout: post
title:  "在项目中添加 `package.json`"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '05'
---

管理局部安装包最好的方式是创建一个 `package.json` 文件。

`package.json` 文件会提供给你许多强大的功能：

1. 它可以是你项目依赖包的文档
2. 它允许你使用[版本的语义规则](https://docs.npmjs.com/getting-started/semantic-versioning)为你项目中的包指定版本
3. 让你的项目易于搭建，这意味着你可以很轻松的与其他开发者共同协作。

<h3 id="requirements"><a href="#requirements">必填写的项目</a></h3>

一个 `package.json` 文件至少要有:

- `"name"`
  * 全部小写
  * 只是一个单词，没有空格
  * 连字符 `-` 或者下划线 `_` 均可使用
- `"version"`

例如:

``` json
{
  "name": "my-awesome-package",
  "version": "1.0.0"
}
```

<h3 id="creating-a-package-json"><a href="#creating-a-package-json">创建一个 `package.json`</a></h3>

执行命令创建 `package.json`：

``` bash
npm init
```

这个命令会让你确认或输入一些选项，你确认的这些选项会被保存到这个目录的 `package.json` 文件中、

<h3 id="the-yes-init-flag"><a href="#the-yes-init-flag">`--yes` 初始化标记</a></h3>

这些扩展的CLI问答显然并不适合所有人，有时候你可能只需要利用 `package.json` 的便捷为你提供更快的体验。

你可以在执行 `npm init` 时添加 `--yes` 或者 `-y` 参数来生成一个默认的 `package.json` 文件：

``` bash
npm init --yes
```

这样执行时，就只会询问你一个问题， `author`（作者）, 其余会被填充默认值。

``` bash
> npm init --yes
Wrote to /home/ag_dubs/my_package/package.json:

{
  "name": "my_package",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "ag_dubs",
  "license": "ISC",
  "repository": {
    "type": "git",
    "url": "https://github.com/ashleygwilliams/my_package.git"
  },
  "bugs": {
    "url": "https://github.com/ashleygwilliams/my_package/issues"
  },
  "homepage": "https://github.com/ashleygwilliams/my_package"
}
```

- `name`：在一个 git 目录下是这个仓库的名字，其他情况下默认为作者名称
- `version`：总是 `1.0.0`
- `main`：总是为 `main.js`
- `script`：默认创建一个空的 `test` 脚本命令
- `keywords`： 空
- `author`：就是你在命令行中输入的
- `license`：`[ISC](https://opensource.org/licenses/ISC)`
- `repository`: 如果有，则会从当前目录下拉取信息
- `bugs`: 如果有，则会从当前目录下拉取信息
- `homepage`: 如果有，则会从当前目录下拉取信息

你也可以为 init 命令设置一些配置项，例如：

``` bash
npm set init.author.email "wombat@npmjs.com"
npm set init.author.name "ag_dubs"
npm set init.license "MIT"
```

<a href="#NOTE" id="NOTE">**注意**</a>

如果 `package.json` 中没有描述的字段，npm 会使用 [README.md](https://github.com/echonest/pyechonest/blob/master/README.md)文件的第一行或者 README 来代替。这些描述会帮助人们在使用 npm 的搜索功能时找到你发布的包，所以如果你希望你发布的包能被更容易的检索到，在 package.json 中编写描述信息是十分有用的。

<h3 id="specifying-packages"><a href="#specifying-packages">在 package.json 中设定包</a></h3>

为了设置你项目依赖的包，你需要将你想要用的包列在 `package.json` 文件中，你可以列出两种类型的包：

- `"dependencies"`: 这些包是你的应用在生产环境中所需要的
- `"devDependencies"`: 这些包只用于开发和测试

<h4 id="manually-editing-your-package-json"><a href="#manually-editing-your-package-json">手动编辑你的 `package.json`</a></h4>

你可以编辑你的 `package.json`文件。 创建一个属性名为 `dependencies` 对象，这个对象中的属性名就是你想使用的包的名称，而对应的值则是符合 [semver](https://docs.npmjs.com/getting-started/semantic-versioning) 描述的与你的项目兼容的版本。

如果你拥有只会在本地开发环境下才会依赖的包，你可用如同上面那样把他们依赖到属性为 `devDependencies` 的对象中。

例如：项目中可以使用主版本号是 1 的任意 `my_dep` 包。而且依赖主版本号是 3 的任意 `my_test_framework` 包，但只用于开发：

``` json
{
  "name": "my_package",
  "version": "1.0.0",
  "dependencies": {
    "my_dep": "^1.0.0"
  },
  "devDependencies" : {
    "my_test_framework": "^3.1.0"
  }
}
```

<h3 id="the-save-and-save-dev-install-flags"><a href="#the-save-and-save-dev-install-flags">安装参数 `--save` 和 `--save-dev`</a></h3>

将依赖添加进 `package.json` 中最简单也是最好的方法是使用命令行，在执行 `npm install` 命令时添加 `--save` 或 `--save-dev` 参数就会按照你的使用习惯添加进依赖中。

向 `package.json` 的 `dependencies` 中添加

``` bash
npm install <package_name> --save
```

向 `package.json` 的 `devDependencies` 中添加

``` bash
npm install <package_name> --save-dev
```

<h3 id="managing-dependency-versions"><a href="#managing-dependency-versions">管理依赖的版本</a></h3>

npm 使用语义化版本声明，即我们通常所说的，SemVer，来管理包的版本和版本区间。

如果你的项目目录中有一个 `package.json` 文件并且执行 `npm install`，之后 npm 会查看依赖中列出的包，并下载符合 [semver 规则](https://docs.npmjs.com/getting-started/semantic-versioning)的他们的最新版本。

学习更多关于语义版本的内容，请查看我们的[开始使用 - Semver页面](https://docs.npmjs.com/getting-started/semantic-versioning).
