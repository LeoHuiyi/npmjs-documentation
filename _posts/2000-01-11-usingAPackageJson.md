---
layout: post
title:  "在项目中添加一个 `package.json` 文件"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'getting-started'
order: '05'
---

四个相同的链接需要替换

管理局部安装包最好的方式是创建一个 `package.json` 文件。

`package.json` 文件会提供给你许多强大的功能：

1. 它可以是你项目依赖包的文档
2.它允许你使用[版本的语义规则](https://docs.npmjs.com/getting-started/semantic-versioning)为你项目中的包指定版本
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

这个命令会让你确认或输入一些选项，你确认的这些选项会包含在这个目录的 `package.json` 文件中、


<h3 id="the-yes-init-flag"><a href="#the-yes-init-flag">`--yes` 初始化标记</a></h3>

这些扩展的CLI问答显然并不适合所有人，有时候你可能只需要利用 `package.json` 的便捷为你提供个快的体验。

你可以在执行 `npm init` 时添加 `--yes` 或者 `-y` 参数来获取一个默认的 `package.json` 文件：

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

<a href="#NOTE" id="NOTE">`注意`</a>

如果 `package.json` 中没有描述的字段，npm 会使用 [README.md](https://github.com/echonest/pyechonest/blob/master/README.md)文件的第一行或者 README 来代替。这些描述会帮助人们在使用 npm 的搜索功能时找到你发布的包，所以如果你希望的包能被更容易的检索到，在 package.json 中编写描述信息是十分有用的。

<h3 id="specifying-packages"><a href="#specifying-packages">在 package.json 中设定包</a></h3>

为了设置你项目依赖的包，你需要将你想要用的包列在 `package.json` 文件中，你可以列出两种类型的包：

- `"dependencies"`: 这些包是你的应用在生产环境中所需要的
- `"devDependencies"`: 这些包只用于开发和测试

<h4 id="manually-editing-your-package-json"><a href="#manually-editing-your-package-json">手动编辑你的 `package.json`</a></h4>

你可以手动编辑你的 `package.json`文件。 You'll need to create an attribute in the package object called `dependencies` that points to an object. This object will hold attributes named after the packages you'd like to use, that point to a [semver](https://docs.npmjs.com/getting-started/semantic-versioning) expression that specifies what versions of that project are compatible with your project.

If you have dependencies you only need to use during local development, you will follow the same instructions as above but in an attribute called `devDependencies`.

For example: The project below uses any version of the package `my_dep` that matches major version 1 in production, and requires any version of the package `my_test_framework` that matches major version 3, but only for development:

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

<h3 id="the-save-and-save-dev-install-flags">[Specifying Packages](#the-save-and-save-dev-install-flags)</h3>

The easier (and more awesome) way to add dependencies to your `package.json` is to do so from the command line, flagging the `npm install` command with either `--save` or `--save-dev`, depending on how you'd like to use that dependency.

To add an entry to your `package.json`'s `dependencies`:

``` bash
npm install <package_name> --save
```

To add an entry to your `package.json`'s `devDependencies`:

``` bash
npm install <package_name> --save-dev
```

<h3 id="managing-dependency-versions">[管理依赖的版本](#managing-dependency-versions)</h3>

npm uses Semantic Versioning, or, as we often refer to it, SemVer, to manage versions and ranges of versions of packages.

If you have a `package.json` file in your directory and you run `npm install`, then npm will look at the dependencies that are listed in that file and download the latest versions satisfying [semver rules](https://docs.npmjs.com/getting-started/semantic-versioning) for all of those.

To learn more about semantic versioning, check out our [Getting Started "Semver" page](https://docs.npmjs.com/getting-started/semantic-versioning).
