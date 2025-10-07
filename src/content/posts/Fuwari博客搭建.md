---
title: Fuwari博客搭建
published: 2025-10-07
description: ''
image: ''
tags:
  - 博客
  - Fuwari
  - Twikoo
category: ''
draft: false 
lang: ''
---

## 博客

前提：
1.git
2.github帐号
3.cloudflare


折腾了这么久，博客和该死的评论终于弄完了。

Fuwari博客还算简单。

[二叉树树的fuwari搭建教程](https://2x.nz/posts/fuwari/)

[fuwari](https://github.com/saicaca/fuwari)这是fuwari的github仓库，点击fork（分叉仓库），Repository name
（仓库名）随便，Description（介绍）随便，Copy the main branch only（仅复制主分支）不勾，点击Create fork。

cmd运行

git clone <你分叉的仓库>

npm install -g pnpm

cd 你分叉的仓库的仓库名

pnpm install（不要运行pnpm add sharp）

....（此处省略，以后在写）


## 添加Twikoo评论支持

这里有两套方案

一个是Giscus，一个是我使用的Twikoo，giscus有个巨大的特点是使用它的博客评论的时候需要登陆github，twikoo不要。

接下来介绍使用twikoo给fuwari提供评论支持。

[Fuwari 主题魔改 - 给你的Fuwari添加Twikoo评论支持](https://www.persicif.xyz/posts/blog-theme-mod/#%E4%B8%BA-fuwari-%E6%8E%A5%E5%85%A5-twikoo)

[Astro | 为 Fuwari 主题添加 Twikoo 评论](https://blog.tantalum.life/posts/add-comments-to-fuwari-with-twikoo/)

在项目目录src/components/comment下创建文件Twikoo.astro文件

[twikoo官方文档](https://twikoo.js.org/frontend.html#%E9%80%9A%E8%BF%87-cdn-%E5%BC%95%E5%85%A5)中cdn引入方式文本

```html
<div id="tcomment"></div>
<script src="https://cdn.jsdelivr.net/npm/twikoo@1.6.44/dist/twikoo.min.js"></script>
<script>
twikoo.init({
  envId: '您的环境id', // 腾讯云环境填 envId；Vercel 环境填地址（https://xxx.vercel.app）
  el: '#tcomment', // 容器元素
  // region: 'ap-guangzhou', // 环境地域，默认为 ap-shanghai，腾讯云环境填 ap-shanghai 或 ap-guangzhou；Vercel 环境不填
  // path: location.pathname, // 用于区分不同文章的自定义 js 路径，如果您的文章路径不是 location.pathname，需传此参数
  // lang: 'zh-CN', // 用于手动设定评论区语言，支持的语言列表 https://github.com/twikoojs/twikoo/blob/main/src/client/utils/i18n/index.js
})
</script>
```

这个官方引入方式修改如下写入Twikoo.astro文件

```astro
---
interface Props {
	path: string;
}

const config = {
	el: "#tcomment",
	path: Astro.props.path,
};
---

<!-- 简化了配置部分的代码，实际上可以把配置文件统一写入fuwari的配置文件统一读取 -->
<div id="tcomment"></div>
<script define:vars={{ config }}>
  function loadTwikoo() {
    const script = document.createElement("script");
    script.src =
      "https://cdn.jsdelivr.net/npm/twikoo@1.6.44/dist/twikoo.min.js";
    script.defer = true;
    script.onload = () => {
      twikoo.init({
        ...config,
        envId: "https://xxx", // 你的envId，获取方法请参照Twikoo文档
        lang: "zh-CN", // 评论区语言
      }); // 传入配置信息
    };
    document.body.appendChild(script);
  }
  document.addEventListener("loadComment", loadTwikoo, { once: true }); // 监听加载评论事件，但是我们只能监听一次，从而避免多次触发。
</script>
```

2025-10-07 未完待续，以后再写