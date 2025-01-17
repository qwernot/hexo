---
title: Hexo 博客技巧：添加自定义 html 页面
date: '2024/01/5 19:00:00'
comments: 是否开启评论(true or false)
top_img: 'https://t.mwm.moe/fj'
cover: 'https://t.mwm.moe/fj'
no_word_count: true <!-- 关闭字数统计 -->
reward: true <!-- 当前文章是否开启打赏 -->
copyright: true <!-- 当前文章是否开启版权声明 -->
categories: 实用技巧
tags:
  - hexo、html
abbrlink: 61663
---

# **前言**

以前收集了很多有趣的 html 特效文件，自己也写过不少，但是这些文件都有一个缺点：只能本地浏览。

很早以前就有一个想法，就是将这些文件部署到网站上供人们随时随地浏览，只是一直没能实现。现在有了自己的博客，正好实现完成这个想法。



# **具体过程**

1. 首先在博客根目录的 `source` 文件夹下，新建一个文件夹用于存放要部署的 HTML 文件：

[![封面](https://img.imgdb.cn/item/600baef43ffa7d37b394b987.png)](https://img.imgdb.cn/item/600baef43ffa7d37b394b987.png)

我这里建了一个叫 `HTML` 的文件夹，里面的子文件夹可以存放各个 HTML 文件，当然也可以只创建一个主文件夹，直接在里面放 HTML 文件。

2. 然后在博客根目录的配置文件`_config.yml` 文件里，设置跳过渲染：

- 单个文件，就写：

```yaml
# 跳过渲染
skip_render: 
  - "xxxx.html"
```

- 如果只创建了一个文件夹，要跳过它目录下所有文件的渲染，就写：

```yaml
# 跳过文件夹下所有文件
skip_render: 
  - "文件夹名/*"
```

- 如果父文件夹下还有子文件夹，就写：

```yaml
# 跳过子文件夹
skip_render: 
  - "文件夹名/子文件夹名/*"
```

- 或更简单粗暴的方式：

```yaml
# 跳过文件夹下所有子文件夹和文件
skip_render: 
  - "文件夹名/**"   
```

3. 最后处理 css、js 文件（这步可以先忽略，直接进行第四步，如果不行再回来设置）

因为 hexo 部署的是静态文件，所有文章的 md 文件会被渲染成 html 文件，
hexo 会帮我们把所有 css、js 文件都加到文章里，我们之前跳过了渲染，所以就需要手动把 css、js 整合到 html 文件里

一般我们的代码就是这种结构：

[![HTML结构](https://img.imgdb.cn/item/600bb0653ffa7d37b395668f.png)](https://img.imgdb.cn/item/600bb0653ffa7d37b395668f.png)

下面处理分两部分：

- css：找到 `index.html` 文件里的语句，如：

```html
<link rel="stylesheet" href="css/xxx.css">    
```

 然后在 css 文件夹中找到对应的文件 `xxx.css`，复制文件内容，把上面的代码改为：

```html
<style> css代码内容 </style>
```

- js：找到 `index.html` 文件里的语句，如：

```html
<script src="js/xxx.js"></script>
```

 然后在 js 文件夹中找到对应的文件 `xxx.js`，复制文件内容，把上面的代码改为：

```html
<script> js代码内容 </script>
```

4. 检验成果

```
hexo clean
hexo g
hexo d
```

部署后来到 [https://xxxxx.github.io/ 存放 html 文件的文件夹 /xxx.html](https://xxxxx.github.io/存放html文件的文件夹/xxx.html)

即可查看到你的自定义 html 页面了！

建议在部署前先试试在本地能否打开，如果不行再按上文修改一次。