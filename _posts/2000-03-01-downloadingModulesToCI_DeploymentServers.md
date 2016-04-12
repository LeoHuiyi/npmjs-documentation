---
layout: post
title:  "将模块下载到 CI / 部署服务器"
date:   2016-03-29 11:55:25 +0800
finished: "☆"
tag: 'private-modules'
order: '02'
---

If you are using deployment servers or testing with CI servers, you'll need a way to download your private modules to those servers. To do this, you can set up an .npmrc file which will authenticate your server with npm.

<h3 id="getting-an-authentication-token"><a href="#getting-an-authentication-token">Getting an authentication token</a></h3>

One of the things that has changed in npm is that we now use auth tokens to authenticate in the CLI. To generate an auth token, you can log in on any machine. You'll end up with a line in your [.npmrc](https://docs.npmjs.com/files/npmrc) file that looks like this:

``` bash
//registry.npmjs.org/:_authToken=00000000-0000-0000-0000-000000000000
```

The token is not derived from your password, but changing your password will invalidate all tokens. The token will be valid until the password is changed. You can also invalidate a single token by logging out on a machine that is logged in with that token.

<h3 id="setting-up-environment-variables"><a href="#setting-up-environment-variables">设置环境变量</a></h3>

To make this more secure when pushing it up to the server, you can set this token as an environment variable on the server. For example, in Heroku you would do this:

``` bash
heroku config:set NPM_TOKEN=00000000-0000-0000-0000-000000000000 --app=application_name
```

You will also need to add this to your environment variables on your development machine. In OSX or Linux, you would add this line to your ~/.profile:

``` javascript
export NPM_TOKEN="00000000-0000-0000-0000-000000000000"
```

然后更新你的环境变量

``` bash
source ~/.profile
```

<h3 id="checking-in-your-npmrc"><a href="#checking-in-your-npmrc">在 `.npmrc` 中查看</a></h3>

Then you can check in the .npmrc file, replacing your token with the environment variable.

``` bash
//registry.npmjs.org/:_authToken=${NPM_TOKEN}
```
