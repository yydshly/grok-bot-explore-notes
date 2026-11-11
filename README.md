# 探索笔记

独立开发者，探索 AI 能力能做出什么值得体验的作品；主线是浏览器里的方块海边城市「海边城市」。

这是一个纯 HTML/CSS 的静态网站，没有构建步骤，GitHub Pages 直接从 `main` 分支根目录发布。

网站按日期整理：首页列出一个个日期，点进某一天，里面是这一天拆过的多个项目。

## 目录

```
index.html              首页：简介、日期入口（最新在上，可按标签筛选）、关于
projects.html           按项目 / 标签看，跳到日期页里对应的那一节
assets/style.css        全站样式
assets/img/             图片（只放自己做的图，压缩到 ~200KB 以内）
days/YYYY-MM-DD.html    一天一页，里面按项目分节
days/_day_template.html 新的一天用的模板
notes/*.html            旧笔记地址，自动跳到新的日期页对应章节
```

## 怎么加新的一天

1. 复制模板：`cp days/_day_template.html days/2026-11-12.html`（文件名用日期）。
2. 改 `<title>`、大标题里的日期、开头那句「这一天做了什么」。
3. 在目录里加上各个项目的标题和锚点，下面按模板复制几个 `<section class="project" id="...">`，把每个项目写进去。
4. 有图片就放进 `assets/img/`，先压缩一下（例如 `convert in.jpg -resize 1200x1200 -quality 80 assets/img/xxx.jpg`），AI 做的图在说明里加 `<span class="ai">AI 生成的样图</span>`。
5. 打开 `index.html`，在 `<ul class="days" id="daylist">` 的**最上面**复制一张日期卡片，改日期、链接、这一天的一句话摘要、里面的项目标题和标签；`data-tags` 里写这一天所有标签（空格分隔），标签按钮会自动出现。
6. 打开 `projects.html`，把新项目加到对应的分类下面（没有的分类就新建一组）。
7. 提交并推送：

```
git add -A && git commit -m "新的一天：YYYY-MM-DD" && git push
```

一两分钟后网站自动更新。

## 怎么在已有的一天里加一个项目

1. 打开那一天的 `days/YYYY-MM-DD.html`，在目录里加一条，再在页面底部（最后一个项目后面）加一个 `<section class="project" id="英文短名">`。
2. 更新首页那张日期卡片：补上项目标题，必要时改一下当天摘要和 `data-tags`。
3. 在 `projects.html` 对应分类下加一条，链接写成 `days/YYYY-MM-DD.html#英文短名`。
4. 提交并推送。

## 写作约定

- 中文为主，说人话，先写结论。
- 别人的帖子只附链接和查看时的数字（写明日期），不转载别人的图片或视频。
- 不放私人信息、账号后台数据和没发出去的草稿。
- 没法确认的事情单独写出来，不要猜成事实。
