---
layout: post
title:  "在项目中添加一个 `package.json` 文件"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'getting-started'
order: '05'
---

四个相同的链接需要替换

The best way to manage locally installed npm packages is to create a `package.json` file.

A `package.json` file affords you a lot of great things:

1. It serves as documentation for what packages your project depends on
2. It allows you to specify the versions of a package that your project can use using [semantic versioning rules](https://docs.npmjs.com/getting-started/semantic-versioning)
3. Makes your build reproducable which means that its way easier to share with other developers.

<h3 id="requirements"><a href="#requirements">Requirements</a></h3>

As a bare minimum, `a package.json` must have:

- `"name"`
  * 全部小写
  * 只是一个单词，没有空格
  * 连字符或者下划线均可使用
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

This will initate a command line questionnaire that will conclude with the creation of a package.json in the directory you initiated the command


<h3 id="the-yes-init-flag"><a href="#the-yes-init-flag">`--yes` 初始化标记</a></h3>

The extended CLI Q&A experience is not for everyone, and often if you are comfortable with using a `package.json` you'd like a more expedited experience.

You can get a default `package.json` by running `npm init` with the `--yes` or `-y` flag:

``` bash
npm init --yes
```

这样就只会询问一个问题， `author`（作者）, 其余会被填充默认值。

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

- `name`：defaults to author name unless in a git directory, in which case it will be the name of the repository
- `version`：总是 `1.0.0`
- `main`：总是为 `main.js`
- `script`：默认创建一个空的 `test` 脚本命令
- `keywords`： 空
- `author`：就是你才命令行中输入的
- `license`：`[ISC](https://opensource.org/licenses/ISC)`
- `repository`: will pull in info from the current directory, if present
- `bugs`: will pull in info from the current directory, if present
- `homepage`: will pull in info from the current directory, if present

You can also set several config options for the init command. Some useful ones:

``` bash
npm set init.author.email "wombat@npmjs.com"
npm set init.author.name "ag_dubs"
npm set init.license "MIT"
```

<a href="#NOTE" id="NOTE">`注意`</a>

If there is no description field in the package.json, npm uses the first line of the [README.md](https://github.com/echonest/pyechonest/blob/master/README.md) or README instead. The description helps people find your package on npm search, so it's definitely useful to make a custom description in the package.json to make your package more discoverable.

<h3 id="specifying-packages"><a href="#specifying-packages">Specifying Packages</a></h3>

To specify the packages your project depends on, you need to list the packages you'd like to use in your `package.json` file. There are 2 types of packages you can list:

- `"dependencies"`: these packages are required by your application in production
- `"devDependencies"`: these packages are only needed for development and testing

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
