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

::github{repo="saicaca/fuwari"}

这是fuwari的github仓库，点击fork（分叉仓库），Repository name

（仓库名）随便，Description（介绍）随便，Copy the main branch only（仅复制主分支）不勾，点击Create fork。

cmd运行

```sh
git clone <你分叉的仓库>

npm install -g pnpm

cd 你分叉的仓库的仓库名

pnpm install（不要运行pnpm add sharp）
```

....（此处省略，以后在写）


## 添加Twikoo评论支持

关于评论这里有两套方案

一个是Giscus，一个是我使用的Twikoo，giscus有个巨大的特点是使用它的博客评论的时候需要登陆github，twikoo不要。

接下来介绍使用twikoo给fuwari提供评论支持。

[云函数部署](https://twikoo.js.org/backend.html#%E4%BA%91%E5%87%BD%E6%95%B0%E9%83%A8%E7%BD%B2)这是官方的教程，可以理解成twikoo存储数据的方式。

大概分为docker和git项目两种。

#### docker可以使用Zeabur或者私有部署。

Docker

```sh
docker run --name twikoo -e TWIKOO_THROTTLE=1000 -p 8080:8080 -v ${PWD}/data:/app/data -d imaegoo/twikoo
```

Docker Compose

```yml
version: '3'
services:
  twikoo:
    image: imaegoo/twikoo
    container_name: twikoo
    restart: unless-stopped
    ports:
      - 8080:8080
    environment:
      TWIKOO_THROTTLE: 1000
    volumes:
      - ./data:/app/data
```
zeabur

```txt
镜像:imaegoo/twikoo
环境变量:TWIKOO_THROTTLE: 1000
端口:8080
卷:/app/data
(资源限制 内存 (Mi)64)
```

#### Vercel 部署

[Vercel 部署](https://twikoo.js.org/backend.html#vercel-%E9%83%A8%E7%BD%B2)

```text
申请 [MongoDB Atlas](https://twikoo.js.org/mongodb-atlas.html) 账号，获取 MongoDB 连接字符串

申请 [Vercel](https://vercel.com/signup) 账号

点击以下按钮将 Twikoo 一键部署到 Vercel

[Deploy](https://vercel.com/import/project?template=https://github.com/twikoojs/twikoo/tree/main/src/server/vercel-min)

进入 Settings(设置) - Environment Variables(环境变量)，添加环境变量 MONGODB_URI，值为前面记录的数据库连接字符串

(默认的连接字符串没有指定数据库名称，Twikoo 会连接到默认的名为 test 的数据库。如果需要在同一个 MongoDB 里运行其他业务或供多个 Twikoo 实例使用，建立加入数据库名称并配置对应的 ACL。)

(mongodb+srv://<db_username>:<db_password>@cluster0.xxxx.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0)

上面这个就是默认的。

如果要设置数据库名称则在cluster0.xxxx.mongodb.net/后面指定数据库名称，如下面的。

(mongodb+srv://<db_username>:<db_password>@cluster0.xxxx.mongodb.net/twikoo_fuwari?retryWrites=true&w=majority&appName=Cluster0)

进入 Settings(设置) - Deployment Protection(部署保护)，设置 Vercel Authentication(Vercel身份验证) 为 Disabled(禁用)，并 Save(保存)

进入 Deployments(部署) , 然后在任意一项后面点击更多（三个点） , 然后点击 Redeploy(重新部署) , 最后点击下面的 Redeploy(重新部署)

进入 Overview(概览)，点击 Domains(域名) 下方的链接，如果环境配置正确，可以看到 “Twikoo 云函数运行正常” 的提示

Vercel Domains(域名)（包含 https:// 前缀，例如 https://xxx.vercel.app）即为您的环境 id
```

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

```astro title="Twikoo.astro"
---
import { commentConfig } from "@/config";

interface Props {
	path: string;
}

const config = {
	...commentConfig.twikoo,
	el: "#tcomment",
	path: Astro.props.path,
};
---

<div id="tcomment"></div>
<script is:inline src="https://cdn.staticfile.org/twikoo/1.6.44/twikoo.all.min.js"></script>
<script is:inline define:vars={{ config }}>
  twikoo.init(config)
</script>
```

在src/components/comment路径下新建index.astro

```astro title="index.astro"
---
import type { CollectionEntry } from "astro:content";
import { commentConfig } from "@/config";
import Twikoo from "./Twikoo.astro";

interface Props {
	post: CollectionEntry<"posts">;
}

const { id, data, slug } = Astro.props.post;

const path = `/posts/${slug}`;
const url = `${Astro.site?.href}${path}`;

let commentService = "";
if (commentConfig?.twikoo) {
	commentService = "twikoo";
}
---
<div class="card-base p-6 mb-4">
  {commentService === 'twikoo' && <Twikoo path={path} />}
  {commentService === '' && null}
</div>
```

然后在 Fuwari 主题的配置文件src/config.ts中的最后添加下述代码来引入commentConfig加载配置：

```ts title="config.ts" ins={6-12}
export const expressiveCodeConfig: ExpressiveCodeConfig = {
	// Note: Some styles (such as background color) are being overridden, see the astro.config.mjs file.
	// Please select a dark theme, as this blog theme currently only supports dark background color
	theme: "github-dark",
};

export const commentConfig: CommentConfig = {
	twikoo: {
		envId: "https://xxx",//您的环境id
		lang: "zh-CN",
	},
};
```

envId这一项填写你的envId，非腾讯云环境的话就是 twikoo 服务的域名。

src/pages/posts/[...slug].astro将 Twikoo 使用的页面路径引入。在顶部也要引入一下index.astro来加载 twikoo 等评论系统可显示的页面配置。

```astro title="[...slug].astro" ins={3} {13-15}
---
import path from "node:path";
import Comment from "@components/comment/index.astro"; // twikoo评论
import License from "@components/misc/License.astro";
import Markdown from "@components/misc/Markdown.astro";
import I18nKey from "@i18n/i18nKey";

.....

        </div>
    </div>

    <Comment post={entry}></Comment>
    <!-- twikoo评论 -->

    <div class="flex flex-col md:flex-row justify-between mb-4 gap-4 overflow-hidden w-full">
        <a href={entry.data.nextSlug ? getPostUrlBySlug(entry.data.nextSlug) : "#"}
           class:list={["w-full font-bold overflow-hidden active:scale-95", {"pointer-events-none": !entry.data.nextSlug}]}>
```

最后src/types/config.ts中加入

```ts title="config.ts" ins={6-17}
export type LIGHT_DARK_MODE =
	| typeof LIGHT_MODE
	| typeof DARK_MODE
	| typeof AUTO_MODE;

// twikoo评论
export type CommentConfig = {
	twikoo?: TwikooConfig;
};

type TwikooConfig = {
	envId: string;
	region?: string;
	lang?: string;
};
// twikoo评论结束

```

## 魔改 Twikoo 样式

新建src/styles/twikoo.css

```css title="twikoo.css"
:root {
    --tk-text: black;
  }

  html.dark {
    --tk-text: #d1d5db;
  }

  .tk-comments {
    @apply text-[var(--tk-text)];
  }

  .tk-submit {
    .tk-avatar {
      @apply hidden;
    }
  }

  /* Text Area */
  .tk-row {
    .tk-col {
      @apply flex-col-reverse;
      .tk-input {
        textarea {
          @apply rounded-[var(--radius-large)] py-4 px-6 !min-h-[150px] focus:border-[var(--primary)];
        }
      }
    }
  }

  /* meta input style */
  .tk-meta-input {
    @apply relative mt-3;
    div {
      @apply min-h-10;
      .el-input-group__prepend {
        @apply !bg-inherit rounded-l-lg;
        min-height: inherit;
      }
      input {
        @apply px-4 rounded-r-lg focus:!border-[var(--primary)];
        min-height: inherit;
      }
    }
  }

  /* Button */
  .tk-row.actions {
    @apply w-full !ml-0 !mt-0;
    .__markdown {
      @apply !hidden;
    }
    .tk-preview,
    .tk-send,
    .tk-cancel {
      @apply border-none rounded-lg px-3 py-0 h-8
         !bg-[var(--btn-regular-bg-active)] disabled:!bg-[var(--btn-regular-bg)]
        !text-[var(--btn-content)] disabled:!text-[#ffffffa1];
    }
  }

  /* Comment title */
  .tk-comments-title {
    .__comments svg {
      @apply fill-[var(--primary)];
    }
  }

  .tk-comment {
    @apply border-[1px] border-[rgba(144,147,153,0.31)] p-4 rounded-2xl hover:shadow-md transition-all;
    .tk-action-icon svg {
      @apply fill-[var(--primary)];
    }
  }

  .tk-action {
    .tk-action-count {
      @apply text-[var(--btn-content)];
    }
  }

  .tk-meta {
    .tk-tag {
      @apply border-none rounded-lg text-[var(--btn-content)];
    }

    .tk-tag-green {
      @apply bg-[var(--btn-regular-bg)] dark:bg-[var(--primary)] dark:text-[var(--deep-text)];
    }
  }

  .tk-content,
  .tk-preview-container {
    a {
      @apply link link-underline text-[var(--primary)] font-medium;
    }

    .tk-ruser {
      @apply no-underline;
    }

    :not(pre) > code {
      @apply bg-[var(--inline-code-bg)] rounded-md text-[--inline-code-color] px-1 py-0.5 font-semibold;
    }

    li{
      @apply before:content-['•'] before:text-[var(--primary)];
    }
  }

  /* Replies */
  .tk-replies {
    .tk-comment {
      @apply bg-[var(--page-bg)];
      .tk-content {
        > span:first-of-type {
          @apply text-xs;
        }
      }
    }
  }

  .twikoo .code-block {
    pre {
      @apply !rounded-xl;
    }

    .copy-btn-icon {
      width: inherit !important;
      height: inherit !important;
    }
  }

  .tk-expand-wrap .tk-expand,
  .tk-collapse-wrap .tk-expand {
    @apply hover:rounded-lg mt-1 hover:bg-[var(--btn-plain-bg-hover)];
  }

  /*让表情组件在表情包数量太多的时候正确显示*/
  .card-base {
    overflow: visible;
}

/* 让图片类型表情不换行显示 */
.tk-content img, .tk-preview-container img {
  display: inline;
  vertical-align: bottom !important;
}
```

#### 为评论区添加小标题

修改src\components\comment\Twikoo.astro

HyperCherry的代码我不知道为什么会报错，import WidgetLayout from "@components/widget/WidgetLayout.astro";的引用没有效果。可能我是个废物吧。

```css title="twikoo.css" del={15} ins={2-4} {16} {18-19}
---
import WidgetLayout from "@components/widget/WidgetLayout.astro";
import { commentConfig } from "@/config";
import I18nKey from "@i18n/i18nKey";
import { i18n } from "@i18n/translation";

interface Props {

...


	path: Astro.props.path,
};
---

<WidgetLayout name={i18n(I18nKey.comments)} id="comments">
<div id="tcomment"></div>
</WidgetLayout>

<script is:inline src="https://cdn.staticfile.org/twikoo/1.6.44/twikoo.all.min.js"></script>
<script is:inline define:vars={{ config }}>
  twikoo.init(config)
```

## 解决首次加载不显示,解决评论操作会回到文章顶部

见 [issue #721](https://github.com/twikoojs/twikoo/issues/721)，Twikoo 加了一个href="#"，这是为了防止回复按钮在某些主题（如 VuePress）下被识别为不可点击的链接而加的，不能被官方仓库删除。但是 Fuwari 正是这个href="#"导致了问题。

解：重新编译。

Fork[官方项目](https://github.com/twikoojs/twikoo)

仓库 Clone 到本地

全局删除href="#"

编译出 js 文件（或vercel部署）

编译流程：
```sh
# 安装 yarn（如未安装）
sudo npm install -g yarn
# 安装依赖
yarn install
# 搜索并删除 twikoo 源码中的 href="#"（建议用编辑器全局替换）
# 比如 VS Code 搜索全项目替换为 "javascript:void(0)"或删除，我是都删除了
# 编译（非腾讯云用 twikoo.min.js，全部文件输出在./dist）
yarn build
```

vercel部署

输出目录：./dist

js: 域名/twikoo.min.js

修改src\components\comment\Twikoo.astro

```astro title="Twikoo.astro" del={21-23} ins={24-42}
---
import WidgetLayout from "@components/widget/WidgetLayout.astro";
import I18nKey from "@i18n/i18nKey";
import { i18n } from "@i18n/translation";
import { commentConfig } from "@/config";

interface Props {
	path: string;
}

const config = {
	...commentConfig.twikoo,
	el: "#tcomment",
	path: Astro.props.path,
};
---
<WidgetLayout name={i18n(I18nKey.comments)} id="comments">
<div id="tcomment"></div>
</WidgetLayout>

<script is:inline src="https://cdn.staticfile.org/twikoo/1.6.44/twikoo.all.min.js"></script>
<script is:inline define:vars={{ config }}>
  twikoo.init(config)
<script define:vars={{ config }}>
function loadTwikoo() {

  // 动态加载 Twikoo 脚本，并在加载完成后执行 twikoo.init

  const script = document.createElement('script');
  script.src = 'https://xxx/twikoo.min.js';//js文件
  script.defer = true;
  script.onload = () => {
    if (window.twikoo) {
      window.twikoo.init(config);
    }
  };
  // script.onerror = () => {
  //   console.error('Twikoo script load failed');
  // };
  document.body.appendChild(script);
}
  document.addEventListener("loadComment", loadTwikoo, { once: true }); // 监听加载评论事件，但是我们只能监听一次，从而避免多次触发。
</script>