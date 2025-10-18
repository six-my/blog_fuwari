---
title: dns和私有dns
published: 2025-10-18
description: ""
image: ""
tags:
  - dns
category: ""
draft: false
lang: ""
---
### dns

先解释一下dns是什么,dns是域名系统的缩写.

域名就是像www.zhihu.com这样的东西,dns就是把这玩意解释成ip地址.

比如你访问zhihu.com,会先到dns查询ipv4或ipv6,然后再访问ip地址.

你现在是否有疑问如果dns里没结果或者乱答怎么办

dns查询是有顺序的，电脑会先到本地dns查询，这个是电脑设置的dns或路由器设置的dns或运营商的dns，然后到根dns，顶级域dns，权威dns依次查询

运营商的dns也就是常用的dns了

那么上面的问题就解答了一半了,按照上面的顺序真真的查一遍的话不可能没结果，如果没有结果你查的是域名吗

然后是第二个问题，这里可以参考以下文章

[如何看待三大运营商的域名劫持、DNS 污染等恶心用户的操作？ - 子木Bin的回答 - 知乎](
https://www.zhihu.com/question/398126212/answer/1926934153066177171)

这就是dns污染

2025.10.18 懒得写了,以后在写