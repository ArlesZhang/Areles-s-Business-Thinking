# **完整搭建 Hugo + PaperMod 全流程**

> 该流程已经过笔者 Arles 验证跑通，文章篇幅较长，但**实际配置非常简单**，建议当成字典，**主要看“GitHub Pages 部署核心思路”部分**。

下载资源：[hugo-PaperMod ](https://github.com/adityatelange/hugo-PaperMod)  

## GitHub Pages 部署核心思路

> **核心思路：** 用 Hugo 在本地写好网站（内容+主题），通过 Git 推送到 GitHub 仓库，自动触发 GitHub Pages 生成公开可访问的静态网站。（Git 是管理员）

### 配置流程总览

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


**Git** 在这里的作用，是**将 GitHub、GitHub Pages 与 Hugo 三者高效协同管理起来的“核心控制系统”**。三者如何协同，如下示意图：
```
perl
CopyEdit
         你本地 Hugo 博客项目
                ↓ 修改内容
        ┌──────────────┐
        │     Git      │ ←←←←←←←←←←←←←←←←←←←←←←←←←←←←
        └──────────────┘       版本控制、内容回滚、推送协同
                ↓ push
         ┌──────────────────┐
         │     GitHub       │ ←代码仓库：保存你的 Hugo 项目
         └──────────────────┘
                ↓ 绑定 Pages
         ┌────────────────────┐
         │  GitHub Pages 服务 │ ←自动部署成网页
         └────────────────────┘
                ↓ 公网访问
    https://arleszhang.github.io ← 这是你的博客网址
```


# 开始：从零开始完整部署 Hugo 博客到 GitHub Pages 全流程教程（推荐 PaperMod 主题）

> 本指南适用于：Windows / macOS / Linux 全平台
> 构建方式：**Hugo + PaperMod（主题） → GitHub Pages (main 分支)** 
> 💡 本地写 Markdown，自动部署上线！

---

## 🧱 第 0 步：安装准备

| 工具 | 说明 | 链接 |
| --- | --- | --- |
| ✅ Git | 用于版本控制 + 推送到 GitHub | https://git-scm.com/downloads |
| ✅ Hugo | 用于本地生成博客框架 | https://gohugo.io/getting-started/install/ |
| ✅ GitHub 账号 | 用于托管博客页面 | [https://github.com](https://github.com/) |

---

## 🏗 第 1 步：创建博客项目 + 安装主题

打开终端（Terminal）或 PowerShell，执行以下命令：

```bash
# 1. ~~创建新站点~~
cd D:\03WorkSpace
hugo new site myblog
cd myblog
```
📂 现在你的目录结构如下：
```
myblog/
├── config.toml   ← 空配置文件
├── content/      ← 内容目录
├── themes/       ← 主题目录（等会我们放 PaperMod）
```

✅ Step 1：用 PowerShell 创建 config.toml
powershell
Copy
Edit
cd D:\03WorkSpace\myblog

notepad config.toml
粘贴以下内容进去：

toml
Copy
Edit
baseURL = "http://localhost/"
languageCode = "zh-cn"
title = "我的 Hugo 博客"
theme = "PaperMod"

[params]
  defaultTheme = "auto"
  showReadingTime = true
保存并关闭。


# 2. 下载主题 PaperMod（推荐！美观、简洁、支持夜间模式）

```
git init
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```
💡 这样做的好处是：后续你可以用 git submodule update --remote 一键更新主题。

## ✅第 3 步：复制 exampleSite 内容 

###  **自行获取 ExampleSite 内容**

你需要单独下载或复制 PaperMod 示例站点配置和内容，比如：

- 在 https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite 查找示例配置
- 或者在官方演示站点对应的仓库下载配置文件（如果有）
- 也可以直接从主题的历史版本（旧 release）中提取 `exampleSite`

---

### 具体怎么做？（以 Windows + PowerShell 为例）

假设你的工作目录是：

```
makefile
CopyEdit
D:\03WorkSpace
```

---

方式一：直接克隆 exampleSite 分支（推荐）

```powershell
powershell
CopyEdit
cd D:\03WorkSpace

# 克隆exampleSite分支作为你的完整博客项目
git clone -b exampleSite https://github.com/adityatelange/hugo-PaperMod.git myblog

cd myblog

```

这样你会得到一个完整的 Hugo 博客目录结构，比如：

```
arduino
CopyEdit
myblog/
├── archetypes/
├── assets/
├── content/
├── data/
├── i18n/
├── layouts/
├── static/
├── themes/             ← 包含 PaperMod 主题源码
├── .gitmodules
├── config.yml          ← 这里是 Hugo 配置文件
├── README.md
```

---

方式二：下载 ZIP 解压版

1. 在 https://github.com/adityatelange/hugo-PaperMod ，选择分支切换到 `exampleSite`
2. 点击“Code” → “Download ZIP”
3. 解压 ZIP 文件到：

```
makefile
CopyEdit
D:\03WorkSpace\myblog
```

> 注意：解压时确保 myblog 目录下直接就是上面结构的文件和文件夹，不要把 ZIP 整个文件夹嵌套进去。
> 

---

这两种方式都一样：

- 你得到一个完整的 Hugo 博客站点，包含主题代码（`themes/PaperMod`）和配置文件（`config.yml` 或 `config.toml`），以及内容（`content/`）等
- 不需要你再额外下载主题或复制配置文件
- 目录结构和文件已经帮你准备好了，**可以开箱即用**

---

如何启动博客？

进入项目目录，执行：

```powershell
powershell
CopyEdit
hugo server -D
```

浏览器打开：

```
arduino
CopyEdit
http://localhost:1313/
```

你就看到完整的 PaperMod 博客首页。


## 可能遇到的错误

```
swift
CopyEdit
Error: command error: failed to load modules: module "hugo-PaperMod" not found in "D:\\03WorkSpace\\myblog\\themes\\hugo-PaperMod"; either add it as a Hugo Module or store it in "D:\\03WorkSpace\\myblog\\themes".: module does not exist
```

意思是 Hugo 找不到主题模块 `hugo-PaperMod`，原因通常是：

可能原因

1. **主题目录名称不对**
    
    Hugo 期望主题目录是 `themes/PaperMod`，而错误提示看它在找 `themes/hugo-PaperMod`。
    
2. **配置文件中主题名称配置错误**
    
    你的 `config.yml` 或 `config.toml` 里面 `theme` 配置写成了 `hugo-PaperMod`，但主题目录名字是 `PaperMod`。
    
3. **主题目录实际不存在或为空**
    
    可能你没有完整 clone 或放置主题。
    

---

解决步骤

1. 检查主题目录

确保你的主题目录是：

```
makefile
CopyEdit
D:\03WorkSpace\myblog\themes\PaperMod\
```

而不是 `themes\hugo-PaperMod` 或其他名字。

如果不对，重命名主题目录：

```powershell
powershell
CopyEdit
Rename-Item .\themes\hugo-PaperMod .\themes\PaperMod
```

### 2. 检查配置文件中 theme 配置

打开项目根目录下的 `config.yml`（或者 `config.toml`，看你的配置文件是哪个格式），确保有：

```yaml
yaml
CopyEdit
theme: "PaperMod"
```

或 TOML 格式：

```toml
toml
CopyEdit
theme = "PaperMod"
```

**不要写成** `hugo-PaperMod`。

**最后，检查一下：**

1. `config.yml` 里把

```yaml
yaml
CopyEdit
theme: [hugo-PaperMod]
```

改成

```yaml
yaml
CopyEdit
theme: hugo-PaperMod
```

## ✅ 第 4 步：配置文件调整

现在编辑 `config.toml`，确保包含以下内容（最关键的是 `theme = "PaperMod"`）：

```toml
baseURL = "https://你的用户名.github.io/"  # ⚠️部署到 GitHub Pages 时用你的用户名替换
languageCode = "zh-cn"
title = "我的博客"
theme = "PaperMod"
```

你也可以将配置改为 `config.yaml` 或 `config.json`，但默认 exampleSite 是 TOML 格式。

---

## ✅ 第 5 步：创建一篇新文章

```powershell
hugo new posts/我的第一篇博客.md

```

编辑文章内容：

```markdown
---
title: "我的第一篇博客"
date: 2025-07-30T10:00:00+08:00
draft: false
---

你好，世界！

```

---

## ✅ 第 6 步：本地预览博客

```powershell
hugo server -D
```

打开浏览器访问：

👉 [http://localhost:1313](http://localhost:1313/)

看到 PaperMod 页面就说明成功！

---

## ✅ 第 7 步：部署到 GitHub Pages

### 📦 a. 构建静态页面

```powershell
hugo -D
```

这会在项目根目录下生成一个 `public/` 目录，里面就是最终要部署的 HTML 页面。

---

### 🧱 b. 新建 GitHub 仓库

去 GitHub 创建一个仓库，例如：

```
myblog
```

或者：

```
你的用户名.github.io
```

---

### 🌍 c. 将 `public/` 当作独立仓库部署

```powershell
cd public
git init
git remote add origin https://github.com/你的用户名/你的仓库名.git
git add .
git commit -m "发布博客"
git branch -M main
git push -f origin main
```

---

### 🚀 d. 启用 GitHub Pages

- 打开 GitHub 仓库 → Settings → Pages
- 选择 `Branch: main` → `/ (root)` → Save

> 📢 几分钟后你就可以访问你的博客了：
> ```
> https://你的用户名.github.io/
> ```

---

✅ 总结目录结构

```
myblog/
├── content/posts/我的第一篇博客.md
├── config.toml
├── themes/PaperMod/
├── public/          ← 构建后的静态页面，用于部署
```

## 其他个性化配置

### 🎨 配置博客主题（`config.toml`）

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

### 初始化 Git，并推送代码

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

## ♻️ 持续迭代流程（写→预览→部署）

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
- 响应式设计（手机/电脑均适配）
- 暗色模式支持
- 代码高亮 + 复制按钮
- 清晰的分类 / 标签 / 阅读时间显示
- 公开部署，可作为简历链接、复试展示材料使用

✅ 小结一句话：

> Git 是你博客的大脑，GitHub 是你的仓库，GitHub Pages 是你的传声筒，Hugo 是你的内容生成器。
> 你只需要**专注创作 Markdown 内容**，剩下的 **Git提供版本控制 → Hugo生成静态内容 → GitHub托管代码 → GitHub Actions自动化流程 → GitHub Pages托管结果。** 

