---
title: Fuwari博客搭建和添加Twikoo评论
published: 2025-10-07
description: 关于Fuwari博客搭建和添加Twikoo评论
image: ""
tags:
  - 博客
  - Fuwari
  - Twikoo
category: ""
draft: false
lang: ""
---

## 博客

前提：

1.git

2.github帐号

3.cloudflare

折腾了这么久,博客和该死的评论终于弄完了.

Fuwari博客还算简单.

>参考链接
>
>[二叉树树的fuwari搭建教程](https://2x.nz/posts/fuwari/)

::github{repo="saicaca/fuwari"}

这是fuwari的github仓库,点击fork(分叉仓库),Repository name(仓库名)随便,Description(介绍)随便,Copy the main branch only(仅复制主分支)不勾,点击Create fork.

cmd运行

```sh
git clone <你分叉的仓库>

npm install -g pnpm

cd 你分叉的仓库的仓库名

pnpm install(不要运行pnpm add sharp)
```

....(此处省略,以后在写)

### cloudflare部署玄学问题

```log title="错误日志"
2025-10-07T15:08:34.993563Z	Cloning repository...
2025-10-07T15:08:35.722065Z	From https://github.com/six-my/blog_fuwari
2025-10-07T15:08:35.72253Z	 * branch            2fd99e896043ced38bd6629f70b7580f8fb5c2e9 -> FETCH_HEAD
2025-10-07T15:08:35.722711Z	
2025-10-07T15:08:35.757954Z	HEAD is now at 2fd99e8 更新 Fuwari博客搭建.md
2025-10-07T15:08:35.758384Z	
2025-10-07T15:08:35.838429Z	
2025-10-07T15:08:35.838839Z	Using v2 root directory strategy
2025-10-07T15:08:35.860595Z	Success: Finished cloning repository files
2025-10-07T15:08:37.83636Z	Checking for configuration in a Wrangler configuration file (BETA)
2025-10-07T15:08:37.83693Z	
2025-10-07T15:08:39.038473Z	No wrangler.toml file found. Continuing.
2025-10-07T15:08:39.10401Z	Detected the following tools from environment: pnpm@9.14.4, nodejs@22.16.0
2025-10-07T15:08:39.405655Z	Preparing pnpm@9.14.4 for immediate activation...
2025-10-07T15:08:41.319922Z	Installing project dependencies: pnpm install
2025-10-07T15:08:41.956184Z	Lockfile is up to date, resolution step is skipped
2025-10-07T15:08:42.042467Z	Progress: resolved 1, reused 0, downloaded 0, added 0
2025-10-07T15:08:42.277093Z	Packages: +1095
2025-10-07T15:08:42.277412Z	++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
2025-10-07T15:08:43.043847Z	Progress: resolved 1095, reused 0, downloaded 58, added 52
2025-10-07T15:08:44.044993Z	Progress: resolved 1095, reused 0, downloaded 178, added 176
2025-10-07T15:08:45.045345Z	Progress: resolved 1095, reused 0, downloaded 399, added 395
2025-10-07T15:08:46.045696Z	Progress: resolved 1095, reused 0, downloaded 532, added 533
2025-10-07T15:08:47.046512Z	Progress: resolved 1095, reused 0, downloaded 828, added 830
2025-10-07T15:08:48.046679Z	Progress: resolved 1095, reused 0, downloaded 1007, added 1010
2025-10-07T15:08:49.047526Z	Progress: resolved 1095, reused 0, downloaded 1091, added 1094
2025-10-07T15:08:49.316211Z	Progress: resolved 1095, reused 0, downloaded 1092, added 1095, done
2025-10-07T15:08:49.630395Z	.../.pnpm/swup@4.8.2/node_modules/swup postinstall$ opencollective-postinstall || true
2025-10-07T15:08:49.631167Z	.../esbuild@0.25.10/node_modules/esbuild postinstall$ node install.js
2025-10-07T15:08:49.631917Z	.../sharp@0.34.4/node_modules/sharp install$ node install/check.js
2025-10-07T15:08:49.632475Z	.../node_modules/@parcel/watcher install$ node scripts/build-from-source.js
2025-10-07T15:08:49.733928Z	.../.pnpm/swup@4.8.2/node_modules/swup postinstall: Done
2025-10-07T15:08:49.769214Z	.../esbuild@0.25.10/node_modules/esbuild postinstall: Done
2025-10-07T15:08:49.773334Z	.../node_modules/@parcel/watcher install: Done
2025-10-07T15:08:49.810377Z	.../sharp@0.34.4/node_modules/sharp install: Done
2025-10-07T15:08:49.919559Z	
2025-10-07T15:08:49.919879Z	dependencies:
2025-10-07T15:08:49.919974Z	+ @astrojs/check 0.9.4
2025-10-07T15:08:49.920111Z	+ @astrojs/rss 4.0.12
2025-10-07T15:08:49.920227Z	+ @astrojs/sitemap 3.6.0
2025-10-07T15:08:49.920357Z	+ @astrojs/svelte 7.2.0
2025-10-07T15:08:49.92059Z	+ @astrojs/tailwind 6.0.2
2025-10-07T15:08:49.920734Z	+ @expressive-code/core 0.41.3
2025-10-07T15:08:49.920874Z	+ @expressive-code/plugin-collapsible-sections 0.41.3
2025-10-07T15:08:49.921113Z	+ @expressive-code/plugin-line-numbers 0.41.3
2025-10-07T15:08:49.921249Z	+ @fontsource-variable/jetbrains-mono 5.2.8
2025-10-07T15:08:49.92141Z	+ @fontsource/roboto 5.2.8
2025-10-07T15:08:49.921559Z	+ @iconify-json/fa6-brands 1.2.6
2025-10-07T15:08:49.921697Z	+ @iconify-json/fa6-regular 1.2.4
2025-10-07T15:08:49.921823Z	+ @iconify-json/fa6-solid 1.2.4
2025-10-07T15:08:49.921967Z	+ @iconify-json/material-symbols 1.2.39
2025-10-07T15:08:49.922071Z	+ @iconify/svelte 4.2.0
2025-10-07T15:08:49.922246Z	+ @swup/astro 1.7.0
2025-10-07T15:08:49.922373Z	+ @tailwindcss/typography 0.5.19
2025-10-07T15:08:49.922483Z	+ astro 5.13.10
2025-10-07T15:08:49.922621Z	+ astro-expressive-code 0.41.3
2025-10-07T15:08:49.922773Z	+ astro-icon 1.1.5
2025-10-07T15:08:49.9229Z	+ hastscript 9.0.1
2025-10-07T15:08:49.92303Z	+ katex 0.16.22
2025-10-07T15:08:49.923428Z	+ markdown-it 14.1.0
2025-10-07T15:08:49.923608Z	+ mdast-util-to-string 4.0.0
2025-10-07T15:08:49.924169Z	+ overlayscrollbars 2.12.0
2025-10-07T15:08:49.924407Z	+ pagefind 1.4.0
2025-10-07T15:08:49.924682Z	+ photoswipe 5.4.4
2025-10-07T15:08:49.924819Z	+ reading-time 1.5.0
2025-10-07T15:08:49.924957Z	+ rehype-autolink-headings 7.1.0
2025-10-07T15:08:49.925052Z	+ rehype-components 0.3.0
2025-10-07T15:08:49.925349Z	+ rehype-katex 7.0.1
2025-10-07T15:08:49.925601Z	+ rehype-slug 6.0.0
2025-10-07T15:08:49.925882Z	+ remark-directive 3.0.1
2025-10-07T15:08:49.926027Z	+ remark-directive-rehype 0.4.2
2025-10-07T15:08:49.926169Z	+ remark-github-admonitions-to-directives 1.0.5
2025-10-07T15:08:49.926311Z	+ remark-math 6.0.0
2025-10-07T15:08:49.926467Z	+ remark-sectionize 2.1.0
2025-10-07T15:08:49.926626Z	+ sanitize-html 2.17.0
2025-10-07T15:08:49.926766Z	+ sharp 0.34.4
2025-10-07T15:08:49.926883Z	+ stylus 0.64.0
2025-10-07T15:08:49.927003Z	+ svelte 5.39.6
2025-10-07T15:08:49.92711Z	+ tailwindcss 3.4.17
2025-10-07T15:08:49.92723Z	+ typescript 5.9.2
2025-10-07T15:08:49.927331Z	+ unist-util-visit 5.0.0
2025-10-07T15:08:49.927444Z	
2025-10-07T15:08:49.927573Z	devDependencies:
2025-10-07T15:08:49.927679Z	+ @astrojs/ts-plugin 1.10.4
2025-10-07T15:08:49.927783Z	+ @biomejs/biome 2.2.4
2025-10-07T15:08:49.92788Z	+ @rollup/plugin-yaml 4.1.2
2025-10-07T15:08:49.927971Z	+ @types/hast 3.0.4
2025-10-07T15:08:49.928066Z	+ @types/markdown-it 14.1.2
2025-10-07T15:08:49.92818Z	+ @types/mdast 4.0.4
2025-10-07T15:08:49.928358Z	+ @types/sanitize-html 2.16.0
2025-10-07T15:08:49.928462Z	+ postcss-import 16.1.1
2025-10-07T15:08:49.928706Z	+ postcss-nesting 13.0.2
2025-10-07T15:08:49.92895Z	
2025-10-07T15:08:49.938757Z	Done in 8.3s
2025-10-07T15:08:50.020476Z	Executing user command: pnpm build
2025-10-07T15:08:50.59592Z	
2025-10-07T15:08:50.596156Z	> fuwari@0.0.1 build /opt/buildhome/repo
2025-10-07T15:08:50.596289Z	> astro build && pagefind --site dist
2025-10-07T15:08:50.596386Z	
2025-10-07T15:08:53.297378Z	15:08:53 [vite] Forced re-optimization of dependencies
2025-10-07T15:08:53.723051Z	15:08:53 [content] Syncing content
2025-10-07T15:08:54.907497Z	15:08:54 [content] Synced content
2025-10-07T15:08:54.908369Z	15:08:54 [types] Generated 1.68s
2025-10-07T15:08:54.909282Z	15:08:54 [build] output: "static"
2025-10-07T15:08:54.909453Z	15:08:54 [build] mode: "static"
2025-10-07T15:08:54.909649Z	15:08:54 [build] directory: /opt/buildhome/repo/dist/
2025-10-07T15:08:54.909918Z	15:08:54 [build] Collecting build info...
2025-10-07T15:08:54.910184Z	15:08:54 [build] ✓ Completed in 1.83s.
2025-10-07T15:08:54.910712Z	15:08:54 [build] Building static entrypoints...
2025-10-07T15:08:55.766324Z	Browserslist: browsers data (caniuse-lite) is 8 months old. Please run:
2025-10-07T15:08:55.766944Z	  npx update-browserslist-db@latest
2025-10-07T15:08:55.767374Z	  Why you should do it regularly: https://github.com/browserslist/update-db#readme
2025-10-07T15:08:57.448094Z	15:08:57 [ERROR] [vite] [31m✗[39m Build failed in 2.47s
2025-10-07T15:08:58.370796Z	[vite:css] [postcss] /opt/buildhome/repo/src/styles/markdown.css:23:9: The `link` class does not exist. If `link` is a custom class, make sure it is defined within a `@layer` directive.
2025-10-07T15:08:58.371541Z	file: /opt/buildhome/repo/src/styles/markdown.css:23:8
2025-10-07T15:08:58.371701Z	  Location:
2025-10-07T15:08:58.371809Z	    /opt/buildhome/repo/src/styles/markdown.css:23:8
2025-10-07T15:08:58.371913Z	  Stack trace:
2025-10-07T15:08:58.37201Z	    at Input.error (/opt/buildhome/repo/node_modules/.pnpm/postcss@8.5.6/node_modules/postcss/lib/input.js:135:16)
2025-10-07T15:08:58.372126Z	    at processApply (/opt/buildhome/repo/node_modules/.pnpm/tailwindcss@3.4.17/node_modules/tailwindcss/lib/lib/expandApplyAtRules.js:380:29)
2025-10-07T15:08:58.372253Z	    at /opt/buildhome/repo/node_modules/.pnpm/tailwindcss@3.4.17/node_modules/tailwindcss/lib/processTailwindFeatures.js:55:50
2025-10-07T15:08:58.372362Z	    at async LazyResult.runAsync (/opt/buildhome/repo/node_modules/.pnpm/postcss@8.5.6/node_modules/postcss/lib/lazy-result.js:293:11)
2025-10-07T15:08:58.372481Z	    at async compilePostCSS (file:///opt/buildhome/repo/node_modules/.pnpm/vite@6.3.6_@types+node@24.5.2_jiti@1.21.7_lightningcss@1.29.3_sass@1.80.4_stylus@0.64.0_terser@5.43.1_yaml@2.7.0/node_modules/vite/dist/node/chunks/dep-Bu492Fnd.js:43812:18)
2025-10-07T15:08:58.401826Z	 ELIFECYCLE  Command failed with exit code 1.
2025-10-07T15:08:58.426526Z	Failed: Error while executing user command. Exited with error code: 1
2025-10-07T15:08:58.436062Z	Failed: build command exited with code: 1
2025-10-07T15:08:59.936642Z	Failed: error occurred while running build command
```

```log title="正常日志"
2025-10-07T15:09:40.487126Z	Cloning repository...
2025-10-07T15:09:41.197806Z	From https://github.com/six-my/blog_fuwari
2025-10-07T15:09:41.198302Z	 * branch            2fd99e896043ced38bd6629f70b7580f8fb5c2e9 -> FETCH_HEAD
2025-10-07T15:09:41.198409Z	
2025-10-07T15:09:41.231501Z	HEAD is now at 2fd99e8 更新 Fuwari博客搭建.md
2025-10-07T15:09:41.232214Z	
2025-10-07T15:09:41.310786Z	
2025-10-07T15:09:41.311245Z	Using v2 root directory strategy
2025-10-07T15:09:41.331224Z	Success: Finished cloning repository files
2025-10-07T15:09:43.225244Z	Checking for configuration in a Wrangler configuration file (BETA)
2025-10-07T15:09:43.225875Z	
2025-10-07T15:09:44.361127Z	No wrangler.toml file found. Continuing.
2025-10-07T15:09:44.428508Z	Detected the following tools from environment: pnpm@9.14.4, nodejs@22.16.0
2025-10-07T15:09:44.736421Z	Preparing pnpm@9.14.4 for immediate activation...
2025-10-07T15:09:46.60641Z	Installing project dependencies: pnpm install
2025-10-07T15:09:47.23457Z	Lockfile is up to date, resolution step is skipped
2025-10-07T15:09:47.318271Z	Progress: resolved 1, reused 0, downloaded 0, added 0
2025-10-07T15:09:47.566063Z	Packages: +1095
2025-10-07T15:09:47.566316Z	++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
2025-10-07T15:09:48.319274Z	Progress: resolved 1095, reused 0, downloaded 60, added 50
2025-10-07T15:09:49.319756Z	Progress: resolved 1095, reused 0, downloaded 182, added 182
2025-10-07T15:09:50.320748Z	Progress: resolved 1095, reused 0, downloaded 401, added 397
2025-10-07T15:09:51.321278Z	Progress: resolved 1095, reused 0, downloaded 592, added 595
2025-10-07T15:09:52.321774Z	Progress: resolved 1095, reused 0, downloaded 895, added 897
2025-10-07T15:09:53.328176Z	Progress: resolved 1095, reused 0, downloaded 1051, added 1053
2025-10-07T15:09:54.069771Z	Progress: resolved 1095, reused 0, downloaded 1092, added 1095, done
2025-10-07T15:09:54.368641Z	.../sharp@0.34.4/node_modules/sharp install$ node install/check.js
2025-10-07T15:09:54.369352Z	.../esbuild@0.25.10/node_modules/esbuild postinstall$ node install.js
2025-10-07T15:09:54.369865Z	.../.pnpm/swup@4.8.2/node_modules/swup postinstall$ opencollective-postinstall || true
2025-10-07T15:09:54.370328Z	.../node_modules/@parcel/watcher install$ node scripts/build-from-source.js
2025-10-07T15:09:54.471272Z	.../.pnpm/swup@4.8.2/node_modules/swup postinstall: Done
2025-10-07T15:09:54.487166Z	.../node_modules/@parcel/watcher install: Done
2025-10-07T15:09:54.512543Z	.../esbuild@0.25.10/node_modules/esbuild postinstall: Done
2025-10-07T15:09:54.528296Z	.../sharp@0.34.4/node_modules/sharp install: Done
2025-10-07T15:09:54.66278Z	
2025-10-07T15:09:54.66301Z	dependencies:
2025-10-07T15:09:54.663227Z	+ @astrojs/check 0.9.4
2025-10-07T15:09:54.663515Z	+ @astrojs/rss 4.0.12
2025-10-07T15:09:54.663611Z	+ @astrojs/sitemap 3.6.0
2025-10-07T15:09:54.664144Z	+ @astrojs/svelte 7.2.0
2025-10-07T15:09:54.664331Z	+ @astrojs/tailwind 6.0.2
2025-10-07T15:09:54.66444Z	+ @expressive-code/core 0.41.3
2025-10-07T15:09:54.664556Z	+ @expressive-code/plugin-collapsible-sections 0.41.3
2025-10-07T15:09:54.66476Z	+ @expressive-code/plugin-line-numbers 0.41.3
2025-10-07T15:09:54.665001Z	+ @fontsource-variable/jetbrains-mono 5.2.8
2025-10-07T15:09:54.665159Z	+ @fontsource/roboto 5.2.8
2025-10-07T15:09:54.665301Z	+ @iconify-json/fa6-brands 1.2.6
2025-10-07T15:09:54.665957Z	+ @iconify-json/fa6-regular 1.2.4
2025-10-07T15:09:54.66623Z	+ @iconify-json/fa6-solid 1.2.4
2025-10-07T15:09:54.666352Z	+ @iconify-json/material-symbols 1.2.39
2025-10-07T15:09:54.66647Z	+ @iconify/svelte 4.2.0
2025-10-07T15:09:54.666571Z	+ @swup/astro 1.7.0
2025-10-07T15:09:54.666634Z	+ @tailwindcss/typography 0.5.19
2025-10-07T15:09:54.666746Z	+ astro 5.13.10
2025-10-07T15:09:54.667062Z	+ astro-expressive-code 0.41.3
2025-10-07T15:09:54.667211Z	+ astro-icon 1.1.5
2025-10-07T15:09:54.667361Z	+ hastscript 9.0.1
2025-10-07T15:09:54.667481Z	+ katex 0.16.22
2025-10-07T15:09:54.667589Z	+ markdown-it 14.1.0
2025-10-07T15:09:54.667771Z	+ mdast-util-to-string 4.0.0
2025-10-07T15:09:54.667907Z	+ overlayscrollbars 2.12.0
2025-10-07T15:09:54.668025Z	+ pagefind 1.4.0
2025-10-07T15:09:54.668189Z	+ photoswipe 5.4.4
2025-10-07T15:09:54.668299Z	+ reading-time 1.5.0
2025-10-07T15:09:54.668418Z	+ rehype-autolink-headings 7.1.0
2025-10-07T15:09:54.668551Z	+ rehype-components 0.3.0
2025-10-07T15:09:54.668675Z	+ rehype-katex 7.0.1
2025-10-07T15:09:54.668804Z	+ rehype-slug 6.0.0
2025-10-07T15:09:54.668924Z	+ remark-directive 3.0.1
2025-10-07T15:09:54.669052Z	+ remark-directive-rehype 0.4.2
2025-10-07T15:09:54.66917Z	+ remark-github-admonitions-to-directives 1.0.5
2025-10-07T15:09:54.669288Z	+ remark-math 6.0.0
2025-10-07T15:09:54.669411Z	+ remark-sectionize 2.1.0
2025-10-07T15:09:54.669533Z	+ sanitize-html 2.17.0
2025-10-07T15:09:54.669651Z	+ sharp 0.34.4
2025-10-07T15:09:54.669762Z	+ stylus 0.64.0
2025-10-07T15:09:54.669875Z	+ svelte 5.39.6
2025-10-07T15:09:54.669989Z	+ tailwindcss 3.4.17
2025-10-07T15:09:54.670119Z	+ typescript 5.9.2
2025-10-07T15:09:54.670232Z	+ unist-util-visit 5.0.0
2025-10-07T15:09:54.670344Z	
2025-10-07T15:09:54.670489Z	devDependencies:
2025-10-07T15:09:54.670597Z	+ @astrojs/ts-plugin 1.10.4
2025-10-07T15:09:54.670706Z	+ @biomejs/biome 2.2.4
2025-10-07T15:09:54.670808Z	+ @rollup/plugin-yaml 4.1.2
2025-10-07T15:09:54.670917Z	+ @types/hast 3.0.4
2025-10-07T15:09:54.671016Z	+ @types/markdown-it 14.1.2
2025-10-07T15:09:54.671144Z	+ @types/mdast 4.0.4
2025-10-07T15:09:54.671261Z	+ @types/sanitize-html 2.16.0
2025-10-07T15:09:54.671399Z	+ postcss-import 16.1.1
2025-10-07T15:09:54.671503Z	+ postcss-nesting 13.0.2
2025-10-07T15:09:54.671602Z	
2025-10-07T15:09:54.680243Z	Done in 7.7s
2025-10-07T15:09:54.791195Z	Executing user command: pnpm build
2025-10-07T15:09:55.375357Z	
2025-10-07T15:09:55.375655Z	> fuwari@0.0.1 build /opt/buildhome/repo
2025-10-07T15:09:55.37583Z	> astro build && pagefind --site dist
2025-10-07T15:09:55.375952Z	
2025-10-07T15:09:58.127903Z	15:09:58 [vite] Forced re-optimization of dependencies
2025-10-07T15:09:58.508166Z	15:09:58 [content] Syncing content
2025-10-07T15:09:59.675332Z	15:09:59 [content] Synced content
2025-10-07T15:09:59.675977Z	15:09:59 [types] Generated 1.60s
2025-10-07T15:09:59.676388Z	15:09:59 [build] output: "static"
2025-10-07T15:09:59.676536Z	15:09:59 [build] mode: "static"
2025-10-07T15:09:59.67665Z	15:09:59 [build] directory: /opt/buildhome/repo/dist/
2025-10-07T15:09:59.676783Z	15:09:59 [build] Collecting build info...
2025-10-07T15:09:59.677051Z	15:09:59 [build] ✓ Completed in 1.79s.
2025-10-07T15:09:59.678246Z	15:09:59 [build] Building static entrypoints...
2025-10-07T15:10:00.540422Z	Browserslist: browsers data (caniuse-lite) is 8 months old. Please run:
2025-10-07T15:10:00.540767Z	  npx update-browserslist-db@latest
2025-10-07T15:10:00.541467Z	  Why you should do it regularly: https://github.com/browserslist/update-db#readme
2025-10-07T15:10:04.941227Z	15:10:04 [vite] [32m✓ built in 5.22s[39m
2025-10-07T15:10:04.941549Z	15:10:04 [build] ✓ Completed in 5.26s.
2025-10-07T15:10:04.942223Z	
2025-10-07T15:10:04.942384Z	 building client (vite) 
2025-10-07T15:10:04.965977Z	15:10:04 [vite] transforming...
2025-10-07T15:10:05.918272Z	15:10:05 [vite] [32m✓[39m 161 modules transformed.
2025-10-07T15:10:05.985332Z	15:10:05 [vite] rendering chunks...
2025-10-07T15:10:06.025717Z	15:10:06 [vite] computing gzip size...
2025-10-07T15:10:06.033378Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[32mec.g1fg5.js                                              [39m[1m[2m 0.94 kB[22m[1m[22m
2025-10-07T15:10:06.033675Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[35mLayout.DSulWsr7.css                                      [39m[1m[2m 4.42 kB[22m[1m[22m[2m │ gzip:  1.43 kB[22m
2025-10-07T15:10:06.03383Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[35mLayout.y4KPJ9hc.css                                      [39m[1m[2m14.04 kB[22m[1m[22m[2m │ gzip:  2.61 kB[22m
2025-10-07T15:10:06.034112Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[35mec.4fsv9.css                                             [39m[1m[2m19.69 kB[22m[1m[22m[2m │ gzip:  4.40 kB[22m
2025-10-07T15:10:06.034262Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36murl-utils.XJ5J4WKD.js                                    [39m[1m[2m 0.30 kB[22m[1m[22m[2m │ gzip:  0.21 kB[22m
2025-10-07T15:10:06.034456Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36minput.Hnzv6hqa.js                                        [39m[1m[2m 0.75 kB[22m[1m[22m[2m │ gzip:  0.43 kB[22m
2025-10-07T15:10:06.034593Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36msetting-utils.gDTNN7p4.js                                [39m[1m[2m 1.01 kB[22m[1m[22m[2m │ gzip:  0.50 kB[22m
2025-10-07T15:10:06.034681Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSwupScriptsPlugin.DeeT9ppa.js                            [39m[1m[2m 1.10 kB[22m[1m[22m[2m │ gzip:  0.62 kB[22m
2025-10-07T15:10:06.035069Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mpreload-helper.BlTxHScW.js                               [39m[1m[2m 1.11 kB[22m[1m[22m[2m │ gzip:  0.65 kB[22m
2025-10-07T15:10:06.035277Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mclient.svelte.BsgZq5BR.js                                [39m[1m[2m 1.13 kB[22m[1m[22m[2m │ gzip:  0.63 kB[22m
2025-10-07T15:10:06.035397Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mindex.modern.D46RI4Wq.js                                 [39m[1m[2m 1.77 kB[22m[1m[22m[2m │ gzip:  0.91 kB[22m
2025-10-07T15:10:06.035532Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mpage.Z8IJTFqj.js                                         [39m[1m[2m 2.15 kB[22m[1m[22m[2m │ gzip:  1.01 kB[22m
2025-10-07T15:10:06.035654Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mDisplaySettings.KBDSWvq8.js                              [39m[1m[2m 2.16 kB[22m[1m[22m[2m │ gzip:  1.17 kB[22m
2025-10-07T15:10:06.035828Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSwupHeadPlugin.DvOZNxAa.js                               [39m[1m[2m 2.58 kB[22m[1m[22m[2m │ gzip:  1.28 kB[22m
2025-10-07T15:10:06.035911Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mLightDarkSwitch.BPrEs2E-.js                              [39m[1m[2m 3.33 kB[22m[1m[22m[2m │ gzip:  1.37 kB[22m
2025-10-07T15:10:06.036006Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mArchivePanel.DKaViKlX.js                                 [39m[1m[2m 3.61 kB[22m[1m[22m[2m │ gzip:  1.59 kB[22m
2025-10-07T15:10:06.036133Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36meach.Bn053yMw.js                                         [39m[1m[2m 3.75 kB[22m[1m[22m[2m │ gzip:  1.88 kB[22m
2025-10-07T15:10:06.036419Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSearch.Cbkil6mO.js                                       [39m[1m[2m 4.66 kB[22m[1m[22m[2m │ gzip:  2.05 kB[22m
2025-10-07T15:10:06.036502Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSwupA11yPlugin.BIyElFLX.js                               [39m[1m[2m 5.25 kB[22m[1m[22m[2m │ gzip:  2.12 kB[22m
2025-10-07T15:10:06.036634Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSwupPreloadPlugin.BFr0xV-N.js                            [39m[1m[2m 6.06 kB[22m[1m[22m[2m │ gzip:  2.35 kB[22m
2025-10-07T15:10:06.03671Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mzh_TW.CB2OJO6B.js                                        [39m[1m[2m 7.50 kB[22m[1m[22m[2m │ gzip:  2.59 kB[22m
2025-10-07T15:10:06.036771Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSwupScrollPlugin.DTcbGiCQ.js                             [39m[1m[2m 8.00 kB[22m[1m[22m[2m │ gzip:  2.40 kB[22m
2025-10-07T15:10:06.03685Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mtranslation.B3JIH1NC.js                                  [39m[1m[2m 9.60 kB[22m[1m[22m[2m │ gzip:  4.43 kB[22m
2025-10-07T15:10:06.036983Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mLayout.astro_astro_type_script_index_0_lang.DAHrxWCB.js  [39m[1m[2m16.69 kB[22m[1m[22m[2m │ gzip:  5.41 kB[22m
2025-10-07T15:10:06.03713Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mIcon.BQfpPy5K.js                                         [39m[1m[2m20.41 kB[22m[1m[22m[2m │ gzip:  8.23 kB[22m
2025-10-07T15:10:06.037267Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mSwup.BWOMRtvc.js                                         [39m[1m[2m21.62 kB[22m[1m[22m[2m │ gzip:  7.41 kB[22m
2025-10-07T15:10:06.037372Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mrender.D1qfsYaO.js                                       [39m[1m[2m27.45 kB[22m[1m[22m[2m │ gzip: 10.84 kB[22m
2025-10-07T15:10:06.037485Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mLayout.astro_astro_type_script_index_1_lang.BuSaD_bf.js  [39m[1m[2m31.87 kB[22m[1m[22m[2m │ gzip: 15.37 kB[22m
2025-10-07T15:10:06.037583Z	15:10:06 [vite] [2mdist/[22m[2m_astro/[22m[36mphotoswipe.esm.CKV1Bsxh.js                               [39m[1m[2m60.41 kB[22m[1m[22m[2m │ gzip: 17.48 kB[22m
2025-10-07T15:10:06.037683Z	15:10:06 [vite] [32m✓ built in 1.07s[39m
2025-10-07T15:10:06.050416Z	
2025-10-07T15:10:06.050611Z	 generating static routes 
2025-10-07T15:10:06.167688Z	15:10:06 ▶ src/pages/about.astro
2025-10-07T15:10:06.195392Z	15:10:06   └─ /about/index.html (+27ms) 
2025-10-07T15:10:06.196821Z	15:10:06 ▶ src/pages/archive.astro
2025-10-07T15:10:06.202357Z	15:10:06   └─ /archive/index.html (+5ms) 
2025-10-07T15:10:06.206495Z	15:10:06 ▶ src/pages/posts/[...slug].astro
2025-10-07T15:10:06.214909Z	15:10:06   ├─ /posts/fuwari博客搭建/index.html (+7ms) 
2025-10-07T15:10:06.21933Z	15:10:06   └─ /posts/关于我的博客/index.html (+4ms) 
2025-10-07T15:10:06.220845Z	15:10:06 λ src/pages/robots.txt.ts
2025-10-07T15:10:06.222351Z	15:10:06   └─ /robots.txt (+1ms) 
2025-10-07T15:10:06.266533Z	15:10:06 λ src/pages/rss.xml.ts
2025-10-07T15:10:06.290322Z	15:10:06   └─ /rss.xml (+24ms) 
2025-10-07T15:10:06.293591Z	15:10:06 ▶ src/pages/[...page].astro
2025-10-07T15:10:06.305157Z	15:10:06   └─ /index.html (+11ms) 
2025-10-07T15:10:06.305333Z	15:10:06 ✓ Completed in 263ms.
2025-10-07T15:10:06.30547Z	
2025-10-07T15:10:06.30558Z	 generating optimized images 
2025-10-07T15:10:06.351147Z	15:10:06   ▶ /_astro/demo-avatar.CCyIhFxH_1PBeqU.webp (before: 15kB, after: 10kB) (+44ms) (1/1)
2025-10-07T15:10:06.351794Z	15:10:06 ✓ Completed in 45ms.
2025-10-07T15:10:06.352478Z	
2025-10-07T15:10:06.37805Z	15:10:06 [@astrojs/sitemap] `sitemap-index.xml` created at `dist`
2025-10-07T15:10:06.378331Z	15:10:06 [build] 5 page(s) built in 8.49s
2025-10-07T15:10:06.378502Z	15:10:06 [build] Complete!
2025-10-07T15:10:06.497024Z	
2025-10-07T15:10:06.497257Z	Running Pagefind v1.4.0 (Extended)
2025-10-07T15:10:06.497393Z	Running from: "/opt/buildhome/repo"
2025-10-07T15:10:06.497502Z	Source:       "dist"
2025-10-07T15:10:06.497734Z	Output:       "dist/pagefind"
2025-10-07T15:10:06.497873Z	
2025-10-07T15:10:06.497992Z	[Walking source directory]
2025-10-07T15:10:06.499134Z	Found 5 files matching **/*.{html}
2025-10-07T15:10:06.499279Z	
2025-10-07T15:10:06.499415Z	[Parsing files]
2025-10-07T15:10:06.795695Z	Found a data-pagefind-body element on the site.
2025-10-07T15:10:06.796057Z	↳ Ignoring pages without this tag.
2025-10-07T15:10:06.796166Z	
2025-10-07T15:10:06.796395Z	[Reading languages]
2025-10-07T15:10:06.796562Z	Discovered 1 language: zh-cn
2025-10-07T15:10:06.796665Z	
2025-10-07T15:10:06.79683Z	[Building search indexes]
2025-10-07T15:10:06.799391Z	Total: 
2025-10-07T15:10:06.799558Z	  Indexed 1 language
2025-10-07T15:10:06.800143Z	  Indexed 3 pages
2025-10-07T15:10:06.800272Z	  Indexed 805 words
2025-10-07T15:10:06.800908Z	  Indexed 0 filters
2025-10-07T15:10:06.801029Z	  Indexed 0 sorts
2025-10-07T15:10:06.801155Z	Note: Pagefind doesn't support stemming for the language zh-cn. 
2025-10-07T15:10:06.801237Z	Search will still work, but will not match across root words.
2025-10-07T15:10:06.801296Z	Note: Pagefind doesn't support stemming for the language zh-cn. 
2025-10-07T15:10:06.801401Z	Search will still work, but will not match across root words.
2025-10-07T15:10:06.810324Z	
2025-10-07T15:10:06.810464Z	Finished in 0.313 seconds
2025-10-07T15:10:06.841914Z	Finished
2025-10-07T15:10:07.684917Z	Checking for configuration in a Wrangler configuration file (BETA)
2025-10-07T15:10:07.685517Z	
2025-10-07T15:10:08.791904Z	No wrangler.toml file found. Continuing.
2025-10-07T15:10:08.79282Z	Note: No functions dir at /functions found. Skipping.
2025-10-07T15:10:08.792989Z	Validating asset output directory
2025-10-07T15:10:13.945394Z	Deploying your site to Cloudflare's global network...
2025-10-07T15:10:19.922368Z	Uploading... (170/182)
2025-10-07T15:10:20.90351Z	Uploading... (174/182)
2025-10-07T15:10:21.033589Z	Uploading... (178/182)
2025-10-07T15:10:22.762387Z	Uploading... (182/182)
2025-10-07T15:10:22.7627Z	✨ Success! Uploaded 12 files (170 already uploaded) (3.25 sec)
2025-10-07T15:10:22.762866Z	
2025-10-07T15:10:23.265722Z	✨ Upload complete!
2025-10-07T15:10:27.066379Z	Success: Assets published!
2025-10-07T15:10:28.858669Z	Success: Your site was deployed!
```

[Build fails on [vite:css] [postcss]](https://github.com/saicaca/fuwari/issues/528)参考一下

这个要么重复构建,要么在src/styles/markdown.css 的最顶部添加以下行,让构建通过

```css
@import './main.css';
```

当然这或许并不是一个完美的解决办法.

## 添加Twikoo评论支持

关于评论这里有两套方案

一个是Giscus,一个是我使用的Twikoo,giscus有个巨大的特点是使用它的博客评论的时候需要登陆github,而twikoo不要.

接下来介绍使用twikoo给fuwari提供评论支持.

[云函数部署](https://twikoo.js.org/backend.html#%E4%BA%91%E5%87%BD%E6%95%B0%E9%83%A8%E7%BD%B2)这是官方的教程,可以理解成twikoo存储数据的方式.

大概分为docker和后端加数据库两种.

#### docker可以使用Zeabur或者私有部署.

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

docker部署完了之后,zeabur设置域名访问即可.

### 私有部署

```sh
cd /opt
mkdir twikoo
cd twikoo
nano docker-compose.yml
```

docker-compose.yml内容如下：

```yml title="docker-compose.yml"
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

这里参考[Astro | 为 Fuwari 主题添加 Twikoo 评论](https://blog.tantalum.life/posts/add-comments-to-fuwari-with-twikoo/),我没用这种方法就不写了.

### Vercel 部署

我用的方案是官方方案中的vercel方案,使用vercel作后端,MongoDB作数据库.

[Vercel 部署](https://twikoo.js.org/backend.html#vercel-%E9%83%A8%E7%BD%B2)

```text
申请 [MongoDB Atlas](https://twikoo.js.org/mongodb-atlas.html) 账号,获取 MongoDB 连接字符串

申请 [Vercel](https://vercel.com/signup) 账号

点击以下按钮将 Twikoo 一键部署到 Vercel

[Deploy](https://vercel.com/import/project?template=https://github.com/twikoojs/twikoo/tree/main/src/server/vercel-min)

进入 Settings(设置) - Environment Variables(环境变量),添加环境变量 MONGODB_URI,值为前面记录的数据库连接字符串

(默认的连接字符串没有指定数据库名称,Twikoo 会连接到默认的名为 test 的数据库.如果需要在同一个 MongoDB 里运行其他业务或供多个 Twikoo 实例使用,建立加入数据库名称并配置对应的 ACL.)

(mongodb+srv://<db_username>:<db_password>@cluster0.xxxx.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0)

上面这个就是默认的.

如果要设置数据库名称则在cluster0.xxxx.mongodb.net/后面指定数据库名称,如下面的.

(mongodb+srv://<db_username>:<db_password>@cluster0.xxxx.mongodb.net/twikoo_fuwari?retryWrites=true&w=majority&appName=Cluster0)

进入 Settings(设置) - Deployment Protection(部署保护),设置 Vercel Authentication(Vercel身份验证) 为 Disabled(禁用),并 Save(保存)

进入 Deployments(部署) , 然后在任意一项后面点击更多(三个点) , 然后点击 Redeploy(重新部署) , 最后点击下面的 Redeploy(重新部署)

进入 Overview(概览),点击 Domains(域名) 下方的链接,如果环境配置正确,可以看到 “Twikoo 云函数运行正常” 的提示

Vercel Domains(域名)(包含 https:// 前缀,例如 https://xxx.vercel.app)即为您的环境 id
```

vercel是后端,vercel的项目域名是后面的envId,MongoDB是数据库,数据库连接字符串能让后端访问数据库.

vercel弄完了之后,我们来为Fuwari添加Twikoo评论支持

>参考链接
>
>[Fuwari 主题魔改 - 给你的Fuwari添加Twikoo评论支持](https://www.persicif.xyz/posts/blog-theme-mod/#%E4%B8%BA-fuwari-%E6%8E%A5%E5%85%A5-twikoo)
>
>[Astro | 为 Fuwari 主题添加 Twikoo 评论](https://blog.tantalum.life/posts/add-comments-to-fuwari-with-twikoo/)

在项目目录src/components/comment下创建Twikoo.astro文件

[twikoo官方文档](https://twikoo.js.org/frontend.html#%E9%80%9A%E8%BF%87-cdn-%E5%BC%95%E5%85%A5)中cdn引入方式文本

```html
<div id="tcomment"></div>
<script src="https://cdn.jsdelivr.net/npm/twikoo@1.6.44/dist/twikoo.min.js"></script>
<script>
twikoo.init({
  envId: '您的环境id', // 腾讯云环境填 envId；Vercel 环境填地址(https://xxx.vercel.app)
  el: '#tcomment', // 容器元素
  // region: 'ap-guangzhou', // 环境地域,默认为 ap-shanghai,腾讯云环境填 ap-shanghai 或 ap-guangzhou；Vercel 环境不填
  // path: location.pathname, // 用于区分不同文章的自定义 js 路径,如果您的文章路径不是 location.pathname,需传此参数
  // lang: 'zh-CN', // 用于手动设定评论区语言,支持的语言列表 https://github.com/twikoojs/twikoo/blob/main/src/client/utils/i18n/index.js
})
</script>
```

这个官方引入方式修改如下写入Twikoo.astro文件

```astro title="src/components/comment/Twikoo.astro"
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
<script is:inline src="https://cdn.staticfile.org/twikoo/1.6.44/twikoo.all.min.js"></script><!--这个链接里的版本号要改成你后端的版本号-->
<script is:inline define:vars={{ config }}>
  twikoo.init(config)
</script>
```

在src/components/comment路径下新建index.astro

```astro title="src/components/comment/index.astro"
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

```ts title="src/config.ts" ins={6-12}
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

envId这一项填写你的envId,非腾讯云环境的话就是 twikoo 后端服务的域名.

修改src/pages/posts/[...slug].astro将 Twikoo 使用的页面路径引入.在顶部也要引入一下index.astro来加载 twikoo 等评论系统可显示的页面配置.

```astro title="[...slug].astro" ins={3,13-15}
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

保存更改之后本地运行pnpm dev应该能看到posts页面下的文章都能够显示评论了,点击小齿轮图标可以进入管理页面.

这时试着发下评论,如果没问题的话,后端会在数据库里创建数据库.

## 魔改 Twikoo 样式

新建src/styles/twikoo.css

```css title="src/styles/twikoo.css"
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

## 解决首次加载不显示

修改src/layouts/Layout.astro

```astro title="src/layouts/Layout.astro" del={19} ins={1-7,14,20-24}
// 专用于创建loadComment的事件，即通知评论组件进行一次加载
function initCommentComponent() {
  const event = new Event("loadComment");
  document.dispatchEvent(event);
}
// twikoo评论

function init() {
	// disableAnimation()()		// TODO
	loadTheme();
	loadHue();
	initCustomScrollbar();
	showBanner();
	initCommentComponent();  // 调用initCommentComponent()函数，twikoo
}

....

	window.swup.hooks.on('content:replace', initCustomScrollbar)
	// window.swup.hooks.on('content:replace', initCustomScrollbar)
  	window.swup.hooks.on("content:replace", () => {
    	initCustomScrollbar();
    	initCommentComponent(); // 添加代码调用
  	});
	window.swup.hooks.on('visit:start', (visit: {to: {url: string}}) => {
		// change banner height immediately when a link is clicked
		const bodyElement = document.querySelector('body')
```

## 为评论区添加小标题

修改src/components/comment/Twikoo.astro

HyperCherry的代码我不知道为什么会报错,import WidgetLayout from "@components/widget/WidgetLayout.astro";的引用没有效果.可能我是个废物吧.

```css title="src/components/comment/Twikoo.astro" del={15} ins={2-4,16,18-19}
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

见 [issue #721](https://github.com/twikoojs/twikoo/issues/721),Twikoo 加了一个href="#",这是为了防止回复按钮在某些主题(如 VuePress)下被识别为不可点击的链接而加的,不能被官方仓库删除.但是 Fuwari 正是这个href="#"导致了问题.

解：重新编译.

Fork[官方项目](https://github.com/twikoojs/twikoo)

仓库 Clone 到本地

全局删除href="#"

编译出 js 文件(或vercel部署)

编译流程：
```sh
# 安装 yarn(如未安装)
sudo npm install -g yarn
# 安装依赖
yarn install
# 搜索并删除 twikoo 源码中的 href="#"(建议用编辑器全局替换)
# 比如 VS Code 搜索全项目替换为 "javascript:void(0)"或删除,我是都删除了
# 编译(非腾讯云用 twikoo.min.js,全部文件输出在./dist)
yarn build
```

vercel部署

输出目录：./dist

js文件: 域名/twikoo.min.js

修改src/components/comment/Twikoo.astro

```astro title="src/components/comment/Twikoo.astro" del={21-23} ins={24-42}
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

  // 动态加载 Twikoo 脚本,并在加载完成后执行 twikoo.init

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
  document.addEventListener("loadComment", loadTwikoo, { once: true }); // 监听加载评论事件,但是我们只能监听一次,从而避免多次触发.
</script>
```

## Twikoo使用

昵称:显示的名称

邮箱:去Gravatar.com注册账号绑定自己的域名邮箱,在这里填Gravatar的邮箱后会显示Gravatar的头像

网址:点击之后会跳转的网址

