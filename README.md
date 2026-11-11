# 探索笔记

独立开发者，探索 AI 能力能做出什么值得体验的作品；主线是浏览器里的方块海边城市「海边城市」。

网站地址：https://yydshly.github.io/grok-bot-explore-notes/

## 网站是怎么组织的

整个网站只有一个页面 `index.html`（单页应用）：

- 左边是日期列表（手机上是顶部的下拉框），点一个日期，右边直接换成那一天的内容，不跳页。
- 每一天上面有一排项目按钮，点一下跳到那个项目。
- 「按项目看」和「关于」也在同一个页面里。
- 地址栏用 `#` 记住当前位置，可以直接分享，浏览器的后退也能用：
  - `#/2026-11-11` 某一天
  - `#/2026-11-11/cozyycabin` 某一天里的某个项目
  - `#/projects` 按项目看，`#/about` 关于
  - 什么都不带，默认打开最新的一天。

纯 HTML/CSS/JS，没有构建步骤，GitHub Pages 直接从 `main` 分支根目录发布。

## 目录

```
index.html               唯一的页面：日期列表 + 内容区 + 按项目看 + 关于
data/days.json           日期和项目的目录（标题、一句话摘要、项目 id、标签）
content/YYYY-MM-DD.html  每一天的正文，只包含几个 <section class="project">
content/_template.html   新的一天用的模板
assets/style.css         全站样式
assets/img/              图片（只放自己做的图，压缩到 ~200KB 左右）
days/*.html projects.html notes/*.html   旧地址，自动跳到 index.html 里对应的位置
```

## 怎么加新的一天（加一个文件 + 一条目录）

1. 复制模板：`cp content/_template.html content/2026-11-12.html`，按模板的固定结构写（先总结、再细节）：
   - 最上面：「今天一句话」+ 每个项目一张卡片（一句话是什么、一张图、一句对我的价值），点卡片跳到项目。
   - 每个项目 `<section class="project" id="英文短名">` 里按顺序写：
     1. 一句话结论（`.conclusion`，最显眼）
     2. 这是什么（2–3 句大白话）
     3. 对我的价值（最多 3 条，具体到海边城市、X 涨粉、独立开发）
     4. 可扩展方向（3–4 条，按优先级排，第一条标「先做」）
     5. 关键展示（只放 1–3 张最能说明问题的图，放大）
     6. 详细拆解（其余全部内容放进 `<details>`，默认收起：完整图组、表格、方案、没核实的地方）
   - 图片路径从根目录写：`assets/img/xxx.jpg`；AI 做的图在说明里加 `<span class="ai">AI 生成的样图</span>`。
   - 站内跳转写成 `#/2026-11-12/英文短名`。
2. 打开 `data/days.json`，在 `days` 里加一条（顺序随意，页面会自动把最新的排在最上面）：

```json
{
  "date": "2026-11-12",
  "title": "2026年11月12日",
  "summary": "这一天做了什么，一两句话。",
  "projects": [
    {"id": "英文短名", "title": "项目标题", "tags": ["标签1", "标签2"]}
  ]
}
```

   `projects` 里的 `id` 要和 section 的 `id` 一样。标签会自动出现在「按项目看」里。
3. 有图片就放进 `assets/img/`，先压缩（例如 `convert in.jpg -resize 1200x1200 -quality 80 assets/img/xxx.jpg`）。
4. 提交并推送：`git add -A && git commit -m "新的一天：2026-11-12" && git push`，一两分钟后网站自动更新。

在已有的一天里加项目：在那一天的 `content/YYYY-MM-DD.html` 末尾加一个 section，再在 `data/days.json` 那一天的 `projects` 里加一条。

本地预览：因为内容是用 fetch 读进来的，直接双击打开 html 不行，在仓库目录运行 `python3 -m http.server` 再打开 http://localhost:8000 。

## 写作约定

- 中文为主，说人话，先写结论。
- 别人的帖子只附链接和查看时的数字（写明日期），用文字描述画面，不转载别人的图片或视频。
- 不放私人信息、账号后台数据和没发出去的草稿。
- 没法确认的事情单独写出来，不要猜成事实。
