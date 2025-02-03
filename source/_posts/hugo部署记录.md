---
abbrlink: ''
categories: []
date: ''
tags: []
title: Hugo部署记录
updated: ''
---
#### 部署准备

1. 根据官网提示[快速入门 |雨 果 (gohugo.io)](https://gohugo.io/getting-started/quick-start/)  选定windows终端

如果您是 Windows 用户：

- 不要使用命令提示符
- 不要使用 Windows PowerShell
- 从 [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows) 或 Linux 终端（如 WSL 或 Git Bash）运行这些命令

PowerShell 和 Windows PowerShell [是不同的应用程序](https://learn.microsoft.com/en-us/powershell/scripting/whats-new/differences-from-windows-powershell?view=powershell-7.3)。

2. 本机装好git

#### 开始部署

hugo文档有三种部署方式 ，选用Package managers 部署比较简单

Package managers 中有 Chocolatey、Scoop、Winget 三种命令，前两个需要格外安装，第三种自带，选用第三种，运行

```sh
winget install Hugo.Hugo.Extended
```

安装的是hugo的扩展版（Extended），方便以后安装模板。

#### 创建站点

运行这些命令以创建具有 [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) 主题的 Hugo 站点。

```text
hugo new site quickstart  ## quickstart为创建的站点文件夹，可随意改名称
cd quickstart  ##打开文件
git init   ## ./git
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke  ##添加主题 可直接改成自己想要的主题
echo "theme = 'ananke'" >> hugo.toml  ##在hugo.toml中加上主题和名称 可手动加
hugo server  ##本地运行服务
```

通过终端中显示的 URL 查看您的网站。按下可停止 Hugo 的开发服务器。`Ctrl + C`

根据[快速入门 |雨 果 (gohugo.io)](https://gohugo.io/getting-started/quick-start/)

#### 添加文章

向您的网站添加一个新页面。

```text
hugo new content content/posts/my-first-post.md
```

Hugo 在目录中创建了该文件。使用编辑器打开文件。`content/posts`

```text
+++
title = 'My First Post'
date = 2024-01-14T07:07:07+01:00
draft = true   ##发布改成false
+++
```

请注意，[前面的值](https://gohugo.io/content-management/front-matter/)是 。默认情况下，当您构建站点时，Hugo不会发布草稿内容。详细了解[草稿内容、未来内容和过期内容](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)。

用markdown编辑后保存文件，然后启动 Hugo 的开发服务器以查看该站点。您可以运行以下任一命令来包含草稿内容。

```text
hugo server --buildDrafts
hugo server -D
```

通过终端中显示的 URL 查看网站。

#### 修改主题

```html
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke  ##改成想要的主题
echo "theme = 'ananke'" >> hugo.toml  ##在hugo.toml中加上主题和名称 
```

主题配置可根据主题文档来修改

#### 托管到github [在 GitHub Pages 上托管 |雨 果 (gohugo.io)](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

- github创建一个新仓库 创建好后有一个…or create a new repository on the command line

**具体用户名和仓库名根据自己创建的**

```
echo "# test" >> README.md  ##省略
git init  ##前面运行过 不需要再运行
git add README.md  ##不需要运行 改成 git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:user/test.git  
git push -u origin main
```

- 运行之后访问 GitHub 仓库。从主菜单中选择“**设置**”>**“页面**” 把 **Source**部分改成GitHub Actions
- 在本地存储库中创建一个空文件。

```text
.github/workflows/hugo.yaml
```

- 将下面的 YAML 复制并粘贴到您创建的文件中。根据需要更改分支名称和 Hugo 版本。

```yaml
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.128.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb      
      - name: Install Dart Sass
        run: sudo snap install dart-sass
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
          HUGO_ENVIRONMENT: production
          TZ: America/Los_Angeles
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  # Deployment job
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

- 推送到 GitHub

  ```text
  git add .
  git commit -m "add workflow"
  git push -u origin main
  ```
- 从 GitHub 的主菜单中，选择 **Actions** 选择 add workflow

#### 后续文章提交

在本地写完 运行

```text
git add .
git commit -m "add first post"  ##first post 就是之前上面创建的第一遍文章
git push -u origin main
```
