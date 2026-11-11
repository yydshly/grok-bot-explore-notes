# 探索笔记

独立开发者，探索 AI 能力能做出什么值得体验的作品；主线是浏览器里的方块海边城市「海边城市」。

这是一个纯 HTML/CSS 的静态网站，没有构建步骤，GitHub Pages 直接从 `main` 分支根目录发布。

## 目录

```
index.html            首页：简介、笔记列表（按日期，可按标签筛选）、关于
assets/style.css      全站样式
assets/img/           图片（只放自己做的图，压缩到 ~200KB 以内）
notes/                每篇笔记一个 HTML 文件
notes/_template.html  新笔记模板
```

## 怎么加一篇新笔记

1. 复制模板：`cp notes/_template.html notes/2026-11-12-my-topic.html`（文件名用 `日期-英文短名.html`）。
2. 改 `<title>`、`<h1>`、日期标签行和正文。
3. 有图片就放进 `assets/img/`，先压缩一下（例如 `convert in.jpg -resize 1200x1200 -quality 80 assets/img/xxx.jpg`），AI 做的图在说明里加 `<span class="ai">AI 生成的样图</span>`。
4. 打开 `index.html`，在 `<ul class="notes" id="notelist">` 的**最上面**复制一个 `<li>`，改日期、链接、标题、一句话摘要；`data-tags` 里写标签（空格分隔），标签按钮会自动出现。
5. 提交并推送：

```
git add -A && git commit -m "新笔记：xxx" && git push
```

一两分钟后网站自动更新。

## 写作约定

- 中文为主，说人话，先写结论。
- 别人的帖子只附链接和查看时的数字（写明日期），不转载别人的图片或视频。
- 不放私人信息、账号后台数据和没发出去的草稿。
- 没法确认的事情单独写出来，不要猜成事实。
