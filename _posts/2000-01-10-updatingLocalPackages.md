---
layout: post
title:  "更新安装在局部的包"
date:   2016-03-29 11:55:25 +0800
finished: "★"
tag: 'getting-started'
order: '06'
---
每隔一段时间就应该更新你所依赖的包，这样就能及时获取到上游代码产生的任何更改。

要做到这一点，你只需在 `package.json` 所在的目录下运行 `npm update` 即可。

测试：运行 `npm outdated`，就没有过期提示了。
