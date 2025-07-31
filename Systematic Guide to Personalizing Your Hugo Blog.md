# 🧭 个性化 Hugo 博客的完整系统化指南（基于 PaperMod）

> 我的博客定制“施工蓝图”

---

## ✅ 阶段1：准备工作确认

> 确保你已有以下目录结构（myblog/为博客根目录）：

```
myblog/
├── config.toml / config.yaml       👈 站点配置文件
├── content/                        👈 文章目录
├── themes/
│   └── PaperMod/                   👈 主题目录
├── static/                         👈 静态资源（如图标、头像、css）
└── layouts/                        👈 可选：自定义布局目录

```

---

## ✅ 阶段2：核心个性化目标与路径总览

| 项目 | 操作 | 说明 |
| --- | --- | --- |
| 🎨 主题颜色 | 修改 `custom.css` 或选择暗/亮模式 | 自定义视觉风格 |
| 🏠 首页信息 | 修改 `config.toml` 中的参数 | 改标题、副标题、社交链接等 |
| 🧾 博客结构 | 设置菜单栏（About、Tags、Search） | 增加页面导航 |
| ✍️ 内容创作 | 撰写 `.md` 文件放入 `content/` | 写博客文章 |
| 📸 图标头像 | 替换 `static/` 下的图片 | 个性化头像/logo |
| 💬 评论系统 | 配置 Waline / Disqus / Giscus 等 | 支持互动评论 |
| 📈 SEO 优化 | 设置 `params.seo`, `params.analytics` | 提高搜索引擎排名 |
| 🚀 部署上线 | 配置 GitHub Actions 自动部署 | 持续部署网站 |

---

## 🧱 阶段3：逐步详细操作

---

### ① 修改站点名称、副标题、社交链接等基本信息

### 👉 打开并编辑 `config.yaml`

```YAML
baseURL: "https://ArlesZhang.github.io/"
languageCode: "zh-cn"
title: "Arles Zhang 的技术博客"
theme: hugo-PaperMod
copyright: "© [PaperMod Contributors](https://github.com/adityatelange/hugo-PaperMod/graphs/contributors)"

enableInlineShortcodes: true
enableRobotsTXT: true
buildDrafts: false
buildFuture: false
buildExpired: false
enableEmoji: true
pygmentsUseClasses: true
mainsections: ["posts", "papermod"]

minify:
  disableXML: true

pagination:
  disableAliases: false
  pagerSize: 5

languages:
  en:
    languageName: "English"
    weight: 1
    taxonomies:
      category: categories
      tag: tags
      series: series
    menu:
      main:
        - name: Archive
          url: archives
          weight: 5
        - name: Search
          url: search/
          weight: 10
        - name: Tags
          url: tags/
          weight: 10
        - name: WiKi
          url: https://github.com/adityatelange/hugo-PaperMod/wiki/

  fr:
    languageName: ":fr:"
    weight: 2
    title: PaperModL2
    taxonomies:
      category: FRcategories
      tag: FRtags
      series: FRseries
    menu:
      main:
        - name: Archive
          url: archives/
          weight: 5
        - name: FRTags
          url: frtags
          weight: 10
        - name: FRCategories
          url: frcategories
          weight: 10
        - name: FRSeries
          url: frseries
          weight: 10
        - name: NullLink
          url: "#"
    params:
      languageAltTitle: French
      profileMode:
        enabled: true
        title: PaperMod
        imageUrl: "https://raw.githubusercontent.com/googlefonts/noto-emoji/master/svg/emoji_u1f9d1_1f3fb_200d_1f4bb.svg"
        imageTitle: ProfileMode image
        subtitle: "☄️ Fast | ☁️ Fluent | 🌙 Smooth | 📱 Responsive"
        buttons:
          - name: Blog
            url: posts
          - name: Profile Mode
            url: https://github.com/adityatelange/hugo-PaperMod/wiki/Features#profile-mode

  fa:
    languagedirection: rtl
    weight: 3
    title: PaperMod RTL
    taxonomies:
      category: FAcategories
      tag: FAtags
      series: FAseries
    menu:
      main:
        - name: FATags
          url: fatags
          weight: 10
    params:
      homeInfoParams:
        Title: "Hi there 👋"
        Content: Welcome to RTL layout

outputs:
  home:
    - HTML
    - RSS
    - JSON

params:
  env: production
  author: "Arles Zhang"
  description: "AI 编译器 / 系统方向的成长日志"
  keywords: ["Hugo", "Blog", "PaperMod", "AI 编译器"]
  defaultTheme: auto
  ShowShareButtons: true
  ShowReadingTime: true
  displayFullLangName: true
  ShowPostNavLinks: true
  ShowBreadCrumbs: true
  ShowCodeCopyButtons: true
  ShowRssButtonInSectionTermList: true
  ShowAllPagesInArchive: true
  ShowPageNums: true
  ShowToc: true
  images: ["images/papermod-cover.png"]

  profileMode:
    enabled: true
    title: "欢迎来到我的博客"
    subtitle: "记录 | 分享 | 成长"
    imageUrl: "images/avatar.jpg"
    imageTitle: "头像"
    buttons:
      - name: 博客文章
        url: "/posts"
      - name: GitHub
        url: "https://github.com/ArlesZhang"

  homeInfoParams:
    Title: "欢迎来到 Arles Zhang 的博客"
    Content: >
      👋 这里记录我在 AI、编译器、系统方向的成长与思考  
      🧠 技术沉淀 | 🔬 知识拓展 | 📘 持续输出  

  socialIcons:
    - name: github
      url: "https://github.com/ArlesZhang"
    - name: email
      url: "mailto:arles3427616237@gmail.com"
    - name: medium
      url: "https://medium.com/@arles3427616237"
    - name: zhihu
      url: "https://www.zhihu.com/people/zhang-zhi-hua-20-95"

  editPost:
    URL: "https://github.com/ArlesZhang/ArlesZhang.github.io/tree/main/content"
    Text: "建议修改"
    appendFilePath: true

  assets:
    disableHLJS: true

markup:
  goldmark:
    renderer:
      unsafe: true
  highlight:
    noClasses: false

services:
  instagram:
    disableInlineCSS: true
  x:
    disableInlineCSS: true


```

---

### ② 修改主题样式（自定义字体、颜色等）

### 👉 新建 `assets/css/custom.css`

```css
body {
  font-family: "Segoe UI", "Helvetica Neue", sans-serif;
}

a {
  color: #00bfa5;
}

```

### 👉 修改 `config.toml` 添加样式引用

```toml
[params.assets]
  customCSS = ["css/custom.css"]

```

---

### ③ 新增文章页面结构（About / Tags / Search / Archives）

### 👉 生成页面：

```bash
hugo new about.md
hugo new tags/_index.md
hugo new search.md
hugo new archives.md

```

然后编辑生成的 Markdown 文件，比如 `content/about.md`：

```markdown
---
title: 关于我
type: page
---

你好！我是 Arles Zhang，一名专注于 AI 编译器优化 与 分布式系统方向的研究者与开发者……

```

---

### ④ 写一篇博客文章（Markdown）

```bash
hugo new posts/first-post.md

```

编辑 `content/posts/first-post.md`：

```markdown
---
title: "我与 Hugo 的第一次亲密接触"
date: 2025-07-31
draft: false
---

经过两天努力，我终于成功搭建了自己的技术博客系统，下面记录一下……

```

---

### ⑤ 替换头像 / 图标（提升个性化）

- 放置图片到 `static/images/avatar.jpg`
- 在 `config.toml` 中引用路径为 `images/avatar.jpg`
- 你也可以替换 favicon，放置到 `static/favicon.ico`

---

### ⑥ 开启搜索 / 评论系统

### 搜索支持：

确保你已经生成 `search.md`，再在 `config.toml` 中添加：

```toml
[outputs]
  home = ["HTML", "RSS", "JSON"]

```

### 评论推荐使用 [Waline](https://waline.js.org/) 或 [Giscus](https://giscus.app/)

> 若你有 GitHub 账号，我们后面可以专门开一节帮你集成 Giscus 评论。
> 

---

### ⑦ 自动部署（GitHub Pages + GitHub Actions）

你可以在博客目录下运行：

```bash
hugo server -D

```

然后将 `public/` 文件夹内容推送到 GitHub 的 `gh-pages` 分支，或者使用自动部署流程（我们可以帮你设置 GitHub Actions）。

---

## 📦 阶段4：附加功能（选配）

| 选项 | 实现方式 |
| --- | --- |
| RSS 订阅 | 自动生成，无需配置 |
| 分类目录 | frontmatter 中添加 `categories` |
| 自定义404 | `layouts/404.html` |
| 中文搜索支持 | 引入 `flexsearch` 或 `algolia` |
| 阅读进度条 | JavaScript 插件 |

---

## 🧠 阶段5：思考与提升

你可以开始考虑以下内容，进一步扩展你的 Hugo 博客价值：

1. 如何使用 Hugo 管理科研博客与项目文档？
2. 文章风格与 GitHub 项目如何融合？
3. 如何构建中英文双语的博客系统？

---

## ✅ 下一步推荐执行计划（作为我的待办）

- [ ]  修改 `config.toml` 设置博客基本信息
- [ ]  添加个人头像和 GitHub 社交链接
- [ ]  写一篇 `posts/first-post.md` 博文
- [ ]  配置自定义样式 `assets/css/custom.css`
- [ ]  添加 About / Tags / Search 页面
- [ ]  部署 GitHub Actions 自动部署版本（可选）

---

**进阶计划**：

- 📁 GitHub 仓库文件结构模板
- 📝 `config.toml` 示例完整模板
- 🚀 GitHub Actions 自动部署工作流
- 🎨 个人品牌化建议方案

## 深度定制技巧

### **1. 自定义CSS样式**

创建`assets/css/extended/custom.css`：

```css
/* 修改字体 */
:root {
    --font-headings: "Microsoft YaHei", sans-serif;
}

/* 调整代码块样式 */
pre code {
    border-radius: 8px;
    background: #f8f8f8 !important;
}

```

### **2. 覆盖主题模板**

以修改页脚为例：

```powershell
# 复制页脚模板到本地
mkdir -p layouts/partials/
cp themes/PaperMod/layouts/partials/footer.html layouts/partials/

```

然后编辑`layouts/partials/footer.html`，找到`{{ .Site.Copyright }}`替换为你的版权信息。

### **3. 添加自定义短代码**

创建`layouts/shortcodes/alert.html`：

```html
<div class="alert alert-{{ .Get 0 }}">
  {{ .Inner | markdownify }}
</div>

```

在文章中调用：

```markdown
{{< alert warning >}}
**注意**：这是自定义警告框
{{< /alert >}}

```

---

## **三、内容管理系统化**

### **1. 文章分类管理**

在`content/`中创建分类目录：

```
content/
├── posts/
│   ├── ai/
│   │   └── 深度学习笔记.md
│   └── programming/
│       └── Go语言实践.md
└── about.md

```

在文章Front Matter中添加分类：

```yaml
categories: ["AI"]
tags: ["深度学习", "PyTorch"]

```

### **2. 自动化脚本**

创建`scripts/newpost.ps1`快速生成文章：

```powershell
param($title)
hugo new "posts/$(Get-Date -Format 'yyyy-MM')/$($title.ToLower().Replace(' ','-')).md"

```

用法：

```powershell
./newpost.ps1 "我的新文章"

```

---

## **四、进阶功能集成**

### **1. 添加评论系统 (Utterances)**

在`config.yml`中添加：

```yaml
params:
  comments:
    enabled: true
    utterances:
      repo: 你的GitHub用户名/你的仓库名  # 如：yourname/yourname.github.io

```

### **2. 启用搜索功能**

```yaml
params:
  search:
    enabled: true

```

### **3. SEO优化**

```yaml
params:
  analytics:
    google: "G-XXXXXXXXXX"  # Google Analytics ID
  opengraph:
    enabled: true

```

---

## **五、测试与部署流程**

1. **本地验证**
    
    ```powershell
    hugo server -D --bind=0.0.0.0 --baseURL=http://localhost:1313
    
    ```
    
    - 访问`http://localhost:1313`检查所有修改
2. **提交更改**
    
    ```powershell
    git add .
    git commit -m "完成个性化定制"
    git push origin main
    
    ```
    
3. **检查GitHub Actions**
    - 在仓库的`Actions`标签页查看构建状态
    - 部署完成后访问你的在线博客


## 总体框架总结

```
├── assets/images/  avatar.jpg cover.jpg
│   └── css/
│       └── extended/
│           └── custom.css
├── content/
│   ├── posts/
│   │   ├── ai/深度学习笔记.md
│   │   └── programming/Go语言实践.md
│   └── about.md
└── layouts/
    ├── partials/
    │   └── footer.html
    └── shortcodes/
        └── alert.html

myblog/
├── config.toml / config.yaml 👈 站点配置文件
├── content/                  👈 文章目录
├── themes/
│   └── PaperMod/              👈 主题目录
├── static/    👈静态资源（如图标、头像、css）
└── layouts/   👈可选：自定义布局目录
```






