---
title: "Hugo 搭建个人博客"
date: 2026-06-20
draft: false
description: "利用Hugo搭建属于自己的技术博客知识库"
tags: ["博客", "Hugo", "个人网站"]
categories: ["随笔", "技术"]
cover:
  image: ""
  alt: ""
---

## 为什么选择 Hugo

Hugo 是目前世界上最快的静态网站生成器，相比其他工具具有显著优势：

### Hugo 的核心优势

| 特性 | 说明 |
|---|---|
| **速度** | 构建速度极快，毫秒级完成 |
| **易用** | 无需安装复杂的依赖环境 |
| **Markdown** | 使用 Markdown 编写内容 |
| **主题丰富** | 上百款精美主题可选 |
| **完全免费** | 开源项目，无任何费用 |

### 与其他框架对比

```
构建速度对比（1000篇文章）：
- Hugo:    ~1秒 ⚡⚡⚡⚡⚡
- Hexo:    ~30秒 ⚡⚡
- Jekyll:  ~60秒 ⚡
- Gatsby:  ~120秒
```

## 为什么选择 PaperMod 主题

PaperMod 是一款备受好评的 Hugo 主题，特别适合技术博客：

### 主要特点

- **简洁美观**：界面清爽，阅读体验极佳
- **响应式设计**：完美适配手机、平板、电脑
- **暗色模式**：支持自动切换明暗主题
- **SEO 友好**：对搜索引擎优化友好
- **性能优异**：加载速度快，轻量级
- **功能丰富**：支持代码高亮、目录、标签、分类等

### 主题演示

```yaml
# 主题配置文件示例
params:
  defaultTheme: auto  # 自动切换明暗主题
  author: 你的名字
  description: 博客描述
```

## 本地快速搭建博客

本节详细介绍在 Windows 系统上从零搭建 Hugo 博客的完整步骤。

---

### 准备工作

#### 1. 安装 Git

Git 是版本管理工具，Hugo 主题管理依赖它。

**下载地址：** https://git-scm.com/download/win

**安装后验证：**
```powershell
git --version
```

应该看到类似输出：
```
git version 2.54.0.windows.1
```
---


#### 2. 安装 Hugo（扩展版）

Hugo 扩展版支持 Sass/SCSS 编译，PaperMod 主题需要此功能。

**方法一：使用 Winget（推荐）**
```powershell
# 打开 PowerShell 或命令提示符，运行：
winget install Hugo.Hugo.Extended
```

**方法二：使用 Chocolatey**
```powershell
choco install hugo-extended
```

**方法三：手动安装**
1. 访问 https://github.com/gohugoio/hugo/releases
2. 下载 `hugo_extended_xxx_windows-amd64.zip`
3. 解压到 `D:\Hugo\bin\`
4. 将 `D:\Hugo\bin\` 添加到系统环境变量
   - 右键「此电脑」→ 属性 → 高级系统设置 → 环境变量
   - 编辑 Path → 新建 → 输入 `D:\Hugo\bin\`

**安装后验证：**
```powershell
hugo version
```

应该看到类似输出：
```
hugo v0.163.3-4d22555aebf458d5d150500c9ac4bee5b24cf0d3+extended windows/amd64 BuildDate=2026-06-18T16:18:24Z VendorInfo=gohugoio
```

---

### 第一步：创建博客项目

**1.1 打开命令行工具**

打开 PowerShell 或 Git Bash，进入你想存放博客的目录：

```powershell
# 例如进入 D 盘的 Project 文件夹
cd D:\Project
```

**1.2 创建新网站**

```powershell
hugo new site myblog
```

> `myblog` 是项目名称，可以改成你喜欢的名字

**1.3 进入项目目录**

```powershell
cd myblog
```

**1.4 查看项目结构**

```
myblog/
├── content/        # 博客文章目录
├── layouts/        # 模板布局目录
├── public/        # 构建输出目录（最终发布的网站）
├── static/         # 静态文件目录（图片、CSS、JS 等）
├── themes/         # 主题目录
├── hugo.yaml       # 配置文件（主配置）
└── config.toml     # 配置文件（可选，Toml 格式）
```

---

### 第二步：添加主题

Hugo 主题需要通过 Git 子模块方式安装，这样便于后续更新。

**2.1 初始化 Git 仓库**

```powershell
git init
```

**2.2 添加 PaperMod 主题**

```powershell
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

> 这一步会从 GitHub 下载主题到 `themes/PaperMod` 目录

**2.3 启用主题**

编辑 `hugo.yaml`，添加一行：

```yaml
baseURL: "https://example.com/"
languageCode: "zh-cn"
title: "我的博客"
theme: "PaperMod"
```

---

### 第三步：配置博客

PaperMod 主题推荐使用 `hugo.yaml` 作为配置文件。以下是推荐的基础配置：

```yaml
baseURL: "https://你的用户名.github.io/"
languageCode: "zh-cn"
title: "我的技术博客"
theme: "PaperMod"
defaultContentLanguage: zh
hasCJKLanguage: true

params:
  author: "你的名字"
  description: "分享技术，记录生活"
  defaultTheme: auto  # 自动切换明暗主题
  ShowShareButtons: true  # 显示分享按钮
  ShowReadingTime: true  # 显示阅读时间
  ShowWordCount: true  # 显示字数统计
  displayName: "博客"
  founder: "你的名字"
  websiteTitle: " - 我的技术博客"

menu:
  main:
    - name: 文章
      url: /posts/
      weight: 1
    - name: 标签
      url: /tags/
      weight: 2
    - name: 分类
      url: /categories/
      weight: 3
    - name: 关于
      url: /about/
      weight: 4
```

---

### 第四步：创建文章

**4.1 创建第一篇文章**

```powershell
hugo new posts/hello-world.md
```

> 这会在 `content/posts/` 目录下创建 `hello-world.md` 文件

**4.2 编辑文章**

用任意文本编辑器打开 `content/posts/hello-world.md`，你会看到：

```markdown
---
title: "Hello World"
date: 2026-06-20
draft: false
---

在这里写下你的文章内容...
```

**Front Matter 配置说明：**

| 字段 | 说明 | 示例 |
|---|---|---|
| `title` | 文章标题 | "Hello World" |
| `date` | 发布日期 | 2026-06-20 |
| `draft` | 是否草稿 | false=发布，true=草稿 |
| `description` | 文章描述 | 用于 SEO 显示 |
| `tags` | 标签 | ["技术", "博客"] |
| `categories` | 分类 | ["随笔"] |

**4.3 编写文章内容**

```markdown
---
title: "Hello World"
date: 2026-06-20
draft: false
description: "我的第一篇博客文章"
tags: ["博客", "Hugo"]
categories: ["随笔"]
---

## 文章标题

这是正文内容，支持 **Markdown** 语法。

### 代码示例

    ```python
    print("Hello, Hugo!")
    ```
```

---

### 第五步：本地预览

Hugo 提供实时预览功能，修改内容后浏览器自动刷新。

**5.1 启动预览服务器**

```powershell
hugo server -D
```

> `-D` 参数表示显示草稿文章（draft: true 的文章也会显示）

**5.2 访问预览**

打开浏览器，访问：http://localhost:1313

**5.3 实时预览说明**

| 命令 | 说明 |
|---|---|
| `hugo server` | 普通预览 |
| `hugo server -D` | 显示草稿预览 |
| `hugo server -p 1313` | 指定端口预览 |

修改文章保存后，浏览器会自动刷新显示最新内容。

### 第六步：本地构建

当文章写好后，需要构建生成静态文件才能发布。

**6.1 执行构建**

```powershell
hugo --minify
```

> `--minify` 参数会压缩 HTML、CSS、JS，减小文件体积

**6.2 查看构建结果**

构建完成后，`public/` 目录就是最终要发布的内容：

```
public/
├── index.html          # 首页
├── posts/              # 文章页面
│   ├── hello-world/
│   │   └── index.html
├── css/                # 样式文件
├── js/                 # 脚本文件
└── ...
```

---

### 第七步：常见问题排查

| 问题 | 解决方法 |
|---|---|
| `hugo: command not found` | Hugo 未安装或未添加到 PATH，重启终端试试 |
| 页面空白/无样式 | 确认 `hugo.yaml` 中 `theme: "PaperMod"` 已设置 |
| 主题样式不对 | 检查 `themes/PaperMod` 目录是否存在 |
| 文章不显示 | 确认 `draft: false`，或使用 `hugo server -D` 预览 |

---

### 下一步：部署上线

本地测试满意后，下一步是将网站部署到互联网。

推荐方案：
- **GitHub Pages**：免费，配合 GitHub Actions 自动部署
- **Vercel**：免费，国内访问速度快
- **Netlify**：免费，稳定可靠

详情请参考本文档的「部署到 GitHub Pages」章节。

### 常用命令

| 命令 | 说明 |
|---|---|
| `hugo new site blog` | 创建新网站 |
| `hugo new posts/xxx.md` | 创建新文章 |
| `hugo server` | 本地预览 |
| `hugo --minify` | 构建压缩版 |
| `hugo -D` | 显示草稿 |

## 部署到 GitHub Pages

GitHub Pages 是 GitHub 提供的免费静态网站托管服务，配合 GitHub Actions 可以实现代码推送后自动部署。

---

### 第一步：创建 GitHub 仓库

**1.1 登录 GitHub**

访问 https://github.com 并登录你的账号。

**1.2 创建新仓库**

1. 点击右上角「+」→「New repository」
2. 填写仓库信息：
   - **Repository name**：`你的用户名.github.io`
     > 例如你的 GitHub 用户名是 `john`，就填写 `john.github.io`
   - **Description**：`我的技术博客`（可选）
   - **Visibility**：选择 **Public**（公开）
   - **勾选**「Add a README file」
3. 点击「Create repository」

**1.3 仓库地址**

创建成功后，页面会显示仓库地址，例如：
```
https://github.com/youdward/youdward.github.io
```

---

### 第二步：关联本地仓库

**2.1 添加远程仓库地址**

在项目根目录执行：

```powershell
# 替换为你的实际 GitHub 用户名和仓库名
git remote add origin https://github.com/youdward/youdward.github.io.git
```

**2.2 验证远程仓库**

```powershell
git remote -v
```

应该看到：
```
origin  https://github.com/youdward/youdward.github.io.git (fetch)
origin  https://github.com/youdward/youdward.github.io.git (push)
```

---

### 第三步：创建 GitHub Actions 配置

GitHub Actions 是 GitHub 的自动化工具，可以在你推送代码时自动构建和部署网站。

**3.1 创建工作流目录**

```powershell
mkdir -p .github/workflows
```

**3.2 创建部署配置文件**

在 `.github/workflows/gh-pages.yml` 创建文件，内容如下：

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DART_SASS_VERSION: 1.100.0
      GO_VERSION: 1.26.3
      HUGO_VERSION: 0.163.3
      NODE_VERSION: 24.16.0
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Go
        uses: actions/setup-go@v6
        with:
          go-version: ${{ env.GO_VERSION }}
          cache: false

      - name: Setup Node.js
        uses: actions/setup-node@v6
        with:
          node-version: ${{ env.NODE_VERSION }}

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v6

      - name: Install Dart Sass
        run: |
          curl -sLJO "https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          tar -C "${HOME}/.local" -xf "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          rm "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          echo "${HOME}/.local/dart-sass" >> "${GITHUB_PATH}"

      - name: Install Hugo
        run: |
          curl -sLJO "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          mkdir "${HOME}/.local/hugo"
          tar -C "${HOME}/.local/hugo" -xf "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          rm "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          echo "${HOME}/.local/hugo" >> "${GITHUB_PATH}"

      - name: Verify installations
        run: |
          echo "Dart Sass: $(sass --version)"
          echo "Go: $(go version)"
          echo "Hugo: $(hugo version)"
          echo "Node.js: $(node --version)"

      - name: Build the site
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

---

### 第四步：提交并推送代码

**4.1 创建 .gitignore 文件**

创建 `.gitignore` 文件，避免提交不需要的文件：

```gitignore
# Hugo 构建输出
/public/
/.hugo_build.lock
/resources/

# 操作系统文件
.DS_Store
Thumbs.db

# IDE 配置
.idea/
.vscode/
*.swp
```

**4.2 提交代码**

```powershell
git add .
git commit -m "Initial commit: Hugo blog with PaperMod theme"
```

**4.3 推送到 GitHub**

```powershell
git branch -M main
git push -u origin main
```

> `-u origin main` 会设置上游分支，以后只需 `git push` 即可。

---

### 第五步：启用 GitHub Pages

**5.1 等待 Actions 执行完成**

推送后，打开 GitHub 仓库页面，点击「Actions」标签查看构建状态。

**5.2 启用 Pages**

1. 进入仓库 → Settings → Pages
2. 在「Build and deployment」部分：
   - **Source** 选择：**GitHub Actions**
3. 不需要选择分支（因为我们用的是 Actions 方式）

**5.3 等待部署**

部署通常需要 1-3 分钟。完成后会显示博客访问地址。

---

### 第六步：访问你的博客

部署成功后，访问：`https://你的用户名.github.io/`

例如：`https://youdward.github.io/`

---

### 常见问题排查

| 问题 | 解决方法 |
|---|---|
| Actions 显示红色 ❌ | 点击查看日志，找出错误原因 |
| Pages 一直显示「Pending」 | 等待几分钟，或检查 Actions 是否成功 |
| 页面显示 404 | 确认 baseURL 配置正确 |
| 样式丢失 | 确认 baseURL 以 `/` 结尾 |
| 构建成功但部署失败 | 检查 Pages 设置中的 Source 是否选择 GitHub Actions |

---

### 后续更新博客

以后写完文章，只需：

```powershell
# 1. 提交代码
git add .
git commit -m "更新文章"
git push

# 2. GitHub Actions 会自动构建和部署
# 3. 几分钟后博客就更新了
```

不需要手动构建或上传，自动化完成！

---

## 使用云服务器和自定义域名部署

如果你已经购买了云服务器和域名，可以按照以下步骤在服务器上配置和搭建博客。

> **前提条件**：
> - 已购买云服务器（推荐 Ubuntu 22.04 系统）
> - 已购买域名并完成 ICP 备案（国内服务器需要）
> - 已将域名 A 记录解析到服务器 IP

---

### 第一步：连接服务器

**1.1 获取服务器信息**

记录以下信息：
- **公网 IP**：如 `123.45.67.89`
- **登录用户名**：通常是 `root`
- **登录密码**：购买时设置的密码

**1.2 SSH 连接服务器**

```powershell
# Windows 使用 PowerShell 或 SSH 客户端
ssh root@123.45.67.89

# 输入密码登录
```

---

### 第二步：服务器环境配置

**2.1 更新系统**

```bash
# Ubuntu/Debian
apt update && apt upgrade -y

# CentOS
yum update -y
```

**2.2 安装 Nginx**

```bash
# Ubuntu/Debian
apt install nginx -y

# CentOS
yum install nginx -y

# 启动 Nginx
systemctl start nginx
systemctl enable nginx
```

**2.3 验证 Nginx**

浏览器访问 `http://你的服务器IP`，看到 Nginx 欢迎页说明安装成功。

**2.4 安装 Git 和 Hugo**

```bash
# 安装 Git
apt install git -y

# 安装 Hugo（Ubuntu）
apt install hugo -y

# 或手动安装最新版
wget https://github.com/gohugoio/hugo/releases/download/v0.163.3/hugo_extended_0.163.3_linux-amd64.tar.gz
tar -xzf hugo_extended_0.163.3_linux-amd64.tar.gz
mv hugo /usr/local/bin/

# 验证安装
hugo version
```

---

### 第三步：上传博客文件

**方法一：本地构建后上传（推荐）**

```powershell
# 1. 本地构建
hugo --minify

# 2. 使用 SCP 上传 public 目录到服务器
scp -r public/* root@123.45.67.89:/var/www/html/
```

**方法二：服务器上 Git 拉取并构建**

```bash
# 在服务器上执行
cd /var/www
git clone https://github.com/yourname/yourname.github.io.git blog
cd blog
hugo --minify
cp -r public/* /var/www/html/
```

---

### 第四步：配置 Nginx

**4.1 创建网站配置**

```bash
nano /etc/nginx/sites-available/yourdomain.com
```

写入以下内容：

```nginx
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # 启用 Gzip 压缩
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml;

    # 静态资源缓存
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 30d;
    }
}
```

**4.2 启用配置**

```bash
# 创建软链接
ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/

# 删除默认配置（可选）
rm /etc/nginx/sites-enabled/default

# 测试配置
nginx -t

# 重载 Nginx
systemctl reload nginx
```

---

### 第五步：配置 HTTPS（SSL 证书）

**5.1 安装 Certbot**

```bash
# Ubuntu
apt install certbot python3-certbot-nginx -y

# CentOS
yum install certbot python3-certbot-nginx -y
```

**5.2 申请免费 SSL 证书**

```bash
certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

按提示输入邮箱，同意条款即可。Certbot 会自动修改 Nginx 配置。

**5.3 设置自动续期**

```bash
# 测试续期
certbot renew --dry-run

# 添加定时任务
crontab -e

# 添加以下行（每天凌晨 3 点检查续期）
0 3 * * * certbot renew --quiet
```

**5.4 验证 HTTPS**

访问 `https://yourdomain.com`，浏览器地址栏显示锁图标说明配置成功。

---

### 第六步：配置自动部署（可选）

**6.1 创建部署脚本**

```bash
nano /root/deploy-blog.sh
```

写入以下内容：

```bash
#!/bin/bash
cd /var/www/blog
git pull origin main
hugo --minify
cp -r public/* /var/www/html/
echo "Blog deployed at $(date)"
```

**6.2 设置执行权限**

```bash
chmod +x /root/deploy-blog.sh
```

**6.3 后续更新博客**

每次更新文章后，在服务器执行：

```bash
/root/deploy-blog.sh
```

或者配置 GitHub Webhooks 实现推送后自动触发部署。

---

### GitHub Pages vs 云服务器对比

| 对比项 | GitHub Pages | 云服务器 |
|---|---|---|
| 费用 | 免费 | 150-360 元/年 |
| 配置难度 | 简单 | 中等 |
| 访问速度 | 国内较慢 | 国内快 |
| 自定义域名 | 支持 | 支持 |
| HTTPS | 自动配置 | 需手动配置 |
| 自由度 | 有限制 | 完全自由 |
| 适合人群 | 初学者、个人博客 | 进阶用户、企业网站 |

---

### 最终效果展示

部署完成后，你的博客就可以在互联网上访问了！

<div style="border: 1px solid #e1e4e8; padding: 16px; border-radius: 8px; background-color: #f6f8fa; text-align: center; margin: 16px 0;">
  <p style="margin: 0 0 12px 0; color: #24292e; font-size: 16px; font-weight: bold;">🎉 博客已成功部署</p>
  <a href="https://youdward.github.io/" target="_blank" style="display: inline-block; padding: 10px 20px; background-color: #0366d6; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">访问我的博客 →</a>
  <p style="margin: 8px 0 0 0; color: #586069; font-size: 13px;">https://youdward.github.io/</p>
  <a href="https://youdward.com" target="_blank" style="display: inline-block; padding: 10px 20px; background-color: #28a745; color: white; text-decoration: none; border-radius: 6px; font-size: 14px; margin-top: 12px;">访问自定义域名 →</a>
  <p style="margin: 8px 0 0 0; color: #586069; font-size: 13px;">https://youdward.com</p>
</div>

## 开始写作

现在你可以开始写博客了！推荐的内容方向：

1. **技术笔记**：编程语言、框架、工具使用心得
2. **项目经验**：实战项目总结和问题复盘
3. **知识体系**：整理学习路线和知识框架
4. **生活感悟**：记录成长和思考

### Markdown 写作示例

```markdown
## 二级标题

- 列表项 1
- 列表项 2

**加粗文字** 和 *斜体文字*

[链接文本](https://example.com)

![图片描述](图片路径)
```

> 引用：输出的每一行代码，都是在成为更好的自己的路上。

---

**祝你博客之旅愉快！** 🎉
