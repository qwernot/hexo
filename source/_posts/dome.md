---
abbrlink: '30764'
categories:
- 实用技巧
comments: 是否开启评论(true or false)
copyright: true <!-- 当前文章是否开启版权声明 -->
cover: https://api.r10086.com/%E6%A8%B1%E9%81%93%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87api%E6%8E%A5%E5%8F%A3.php?%E5%9B%BE%E7%89%87%E7%B3%BB%E5%88%97=%E5%8A%A8%E6%BC%AB%E7%BB%BC%E5%90%881
date: 2023/12/29 22:00:00
no_word_count: true <!-- 关闭字数统计 -->
reward: true <!-- 当前文章是否开启打赏 -->
tags:
- hexo、GitHub
title: Hexo+GitHub 搭建个人博客
top_img: https://api.r10086.com/%E6%A8%B1%E9%81%93%E9%9A%8F%E6%9C%BA%E5%9B%BE%E7%89%87api%E6%8E%A5%E5%8F%A3.php?%E5%9B%BE%E7%89%87%E7%B3%BB%E5%88%97=%E5%8A%A8%E6%BC%AB%E7%BB%BC%E5%90%881
updated: '2025-01-19T20:33:09.850+08:00'
---
## 准备工作

安装必要的软件

### Node.js

https://nodejs.org/en/

- Windows：通过 [nvs](https://github.com/jasongin/nvs/)（推荐）或者 [nvm](https://github.com/nvm-sh/nvm) 安装。
- Mac：使用 [Homebrew](https://brew.sh/) 或 [MacPorts](http://www.macports.org/) 安装。
- Linux（DEB/RPM-based）：从 [NodeSource](https://github.com/nodesource/distributions) 安装。
- 其它：使用相应的软件包管理器进行安装，可以参考由 Node.js 提供的 [指导](https://nodejs.org/en/download/package-manager/)。

### git

https://git-scm.com/

- Windows：下载并安装 [git](https://git-scm.com/download/win).
- Mac：使用 [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) 或者下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/)。
- Linux (Ubuntu, Debian)：`sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS)：`sudo yum install git-core`

### 安装 Hexo

官方网址: https://hexo.io/zh-cn/

1. 首先需要建立博客文件夹，建议建在非系统盘，例如 `~E:/Hexo/`，那么这个目录就是我们博客的根目录了。
   因为每个人的命名习惯不同，本帖之后会以 [Blogroot] 指代博客根目录。
2. 使用 npm 安装 Hexo, 在 [Blogroot] 路径下右键 ->Git Bash Here, 输入

```bash
npm config set registry https://registry.npm.taobao.org
#将npm源替换为阿里的镜像。之后的安装就会迅速很多了。
npm install hexo-cli -g
# hexo-cli 是 hexo的指令集。
hexo -v
```

3. 初始化 Hexo 博客：

```bash
## 本地创建一个目录用于存放博客
hexo init
hexo generate
hexo server
```

然后在浏览器中打开 localhost:4000 , 就能看到

[![hello world](https://s2.loli.net/2023/12/31/A3O2fQtZvoUWsDi.png)](https://s2.ax1x.com/2019/04/11/A7DdZq.png)

＞通过以上 3 种方式部署 Hexo 博客之后，就拥有了一个最简单的个人博客网站了，下面讲讲博客的简单初始化。

# Hexo 基础修改

## 修改网站关键信息

Hexo 初始化后，博客网站有一些关键信息是默认的，需要修改为我们自己的信息。

### 网站资料

修改网站各种资料，例如标题、副标题和邮箱等个人资料，请修改博客根目录的站点配置文件 _config.yml：

```yaml
# Site
title: 子墨
subtitle: '一枚乐于分享技术与快乐的博主'
description: ''
keywords:
author: haiyong
language: zh-CN
time
zone: ''
```

### 标签页

进入 Hexo 博客的根目录，执行：

```bash
hexo new page tags
```

打开 `source/tags/index.md` 文件，修改如下：

```markdown
---
title: 标签
date: 2022-03-11 12:53:45
type: "tags"
---
```

### 分类页

进入 Hexo 博客的根目录，执行：

```bash
hexo new page categories
```

打开 `source/categories/index.md 文件`，修改如下：

```markdown
---
title: 分类
date: 2022-03-11 12:56:06
type: "categories"
---
```

### 友情链接

#### 创建友情链接页面

进入 Hexo 博客的根目录，执行：

```bash
hexo new page link
```

打开 `source/link/index.md` 文件，修改如下：

```markdown
---
title: 友情链接
date: 2022-12-11 12:57:48
type: "link"
---
```

#### 友情链接添加

在 Hexo 博客目录中的 `source/_data`（如果没有 _data 文件夹，请自行创建），创建一个文件 `link.yml`

```yaml
- class_name: 本站
  class_desc: 交换友链可在下方评论，或者微信/QQ联系我
  link_list:
    - name: 子墨
      link: https://www.zmnn.fun
      avatar: https://www.zmnn.fun/img/favicon.png
      descr: 一个乐于分享技术与快乐的博主

- class_name: 友情链接
  class_desc: 那些人，那些事
  link_list:
    - name: 三笠ぃ
      link: https://luciferlpc.top/
      avatar: https://luciferlpc.top/img/avatar.jpg
      descr: 好好吃饭🍣 好好睡觉💤 敲敲代码
    - name: iMaeGoo’s Blog
      link: https://www.imaegoo.com
      avatar: https://www.imaegoo.com/images/avatar.jpg
      descr: 虹墨空间站
```

### 关于我

进入 Hexo 博客的根目录，执行：

```bash
hexo new page about
```

打开 `source/about-me/index.md` 文件，修改如下：

```markdown
---
title: 关于作者
date: 2022-03-11 13:01:21
type: "about"
---
```

至此，简单的 Hexo 博客框架就完成搭建了
