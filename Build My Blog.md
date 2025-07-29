# **简易版：完整搭建 Hugo + PaperMod 我的思路**

```
lua
CopyEdit
myblog/
├── themes/
│   └── PaperMod/         ← 下载的主题代码（从 GitHub）
├── content/              ← 内容页面（从 exampleSite 拷贝，或自己创建）  
├── archetypes/           ← 内容模版（可选，也来自 exampleSite）
├── config.yml / toml     ← 关键配置文件（必须指向 theme = 'PaperMod'）

内容扩展
文章：content/posts/文章.md
页面：content/about.md

使用 Hugo 命令快速生成：
powershell
hugo new posts/我的第一篇博客.md
```

然后运行：

```bash
bash
CopyEdit
hugo server -D

```

访问浏览器的：

```
arduino
CopyEdit
http://localhost:1313/
```

✅ 你就看到一个 PaperMod 风格的博客页面了。


# 零基础版：从零开始完整部署 Hugo 博客到 GitHub Pages 全流程教程（推荐 PaperMod 主题）

> 本指南适用于：Windows / macOS / Linux 全平台
> 
> 
> 构建方式：**Hugo + PaperMod（主题） → GitHub Pages (main 分支)** 
> 
> 💡 本地写 Markdown，自动部署上线！
> 

---

## 🧱 第 0 步：安装准备

| 工具 | 说明 | 链接 |
| --- | --- | --- |
| ✅ ~~Git~~ | 用于版本控制 + 推送到 GitHub | https://git-scm.com/downloads |
| ✅ ~~Hugo~~ | 用于本地生成博客框架 | https://gohugo.io/getting-started/install/ |
| ✅ GitHub 账号 | 用于托管博客页面 | [https://github.com](https://github.com/) |

---

## 🏗 第 1 步：创建博客项目 + 安装主题

打开终端（Terminal）或 PowerShell，执行以下命令：

```bash
# 1. ~~创建新站点~~
hugo new site myblog
cd myblog

# 2. 下载主题 PaperMod（推荐！美观、简洁、支持夜间模式）
git init
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

```

https://github.com/adityatelange/hugo-PaperMod/tree/master/layouts

## 🎨 第 2 步：~~配置博客主题~~（`config.toml`）

在 `myblog/` 目录下创建或修改 `config.toml` 文件：

```toml
baseURL = 'https://arleszhang.github.io/'  # 你 GitHub Pages 的网址
languageCode = 'en-us'
title = 'Arles Zhang'
theme = 'PaperMod'

# 开启文章草稿、本地预览、更新时间等
enableRobotsTXT = true
buildDrafts = true
buildFuture = true
buildExpired = true

[params]
  author = "Arles Zhang"
  ShowReadingTime = true
  ShowShareButtons = true
  ShowCodeCopyButtons = true
  ShowPostNavLinks = true
  ShowBreadCrumbs = true
  ShowToc = true
  TocOpen = true

[[menu.main]]
  identifier = "about"
  name = "About"
  url = "/about/"
  weight = 10

[[menu.main]]
  identifier = "posts"
  name = "Posts"
  url = "/posts/"
  weight = 20

```

📂 ~~你还需要复制~~ `themes/PaperMod/exampleSite/content/` 和 `config.yml` 作为初始参考，或者自己新建。

---

## 📝 第 3 步：创作文章（Markdown）

~~新建一篇文章：~~

```bash
hugo new posts/my-first-post.md

```

~~然后编辑~~ `content/posts/my-first-post.md`：

```markdown
---
title: "My First Post"
date: 2025-07-28
draft: false
---

你好，这是我第一篇技术博客！

```bash
# 示例代码块
echo Hello Hugo!

```

```

---

## 🔍 第 4 步：本地预览（开发模式）

```bash
hugo server -D

```

然后访问：`http://localhost:1313` 预览博客。

---

## 🚀 第 5 步：生成静态网页

```bash
hugo

```

它会在 `public/` 目录下生成最终网页。

---

## 🌐 第 6 步：部署到 GitHub Pages

### ✅ 方式一（推荐）：直接部署到主分支 `main`（不使用 gh-pages）

### 1. 创建 GitHub 仓库

在 GitHub 创建仓库：`Arleszhang.github.io`

---

### 2. 初始化 Git，并推送代码

```bash
# 确保你在 myblog 项目目录下
git remote add origin https://github.com/Arleszhang/Arleszhang.github.io
git branch -M main
git add .
git commit -m "Initial Hugo site with PaperMod"
git push -u origin main

```

---

### 3. 设置 GitHub Pages

- 打开 GitHub 仓库
- 进入 **Settings → Pages**
- 将 **Source** 设置为 `Deploy from a branch`
- Branch 选择 `main`，路径选择 `/ (root)`
- 保存

稍等几分钟，访问：

```
https://arleszhang.github.io

```

---

## ♻️ 第 7 步：持续迭代流程（写→预览→部署）

每次写完文章，只需执行：

```bash
# 写文章
hugo new posts/xxx.md

# 本地预览
hugo server -D

# 生成网页
hugo

# 推送到 GitHub
git add .
git commit -m "New blog post"
git push

```

网站自动更新 ✅

---

## ✍️ 目录结构简述

```
myblog/
├── config.toml
├── content/
│   ├── posts/
│   │   └── my-first-post.md
├── themes/
│   └── PaperMod/
├── public/         ← Hugo 构建后的网站文件

```

---

## 📦 可选升级（进阶阶段）

| 功能 | 工具 | 说明 |
| --- | --- | --- |
| 自动部署 | GitHub Actions | 推送后自动构建，不需要本地执行 `hugo` |
| 评论功能 | Disqus / Giscus | 支持访客评论 |
| 搜索功能 | Fuse.js / Algolia | 提升可检索性 |
| 英文页面 | 多语言配置 | 支持 `en` / `zh` 双语 |
| 站点统计 | Google Analytics / Cloudflare | 了解读者来源 |

---

## ✅ 完成后效果参考

> 你的网站将具备：
> 
- 响应式设计（手机/电脑均适配）
- 暗色模式支持
- 代码高亮 + 复制按钮
- 清晰的分类 / 标签 / 阅读时间显示
- 公开部署，可作为简历链接、复试展示材料使用

