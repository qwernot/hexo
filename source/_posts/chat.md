---
title:  利用 API 自己搭建一个 ChatGPT 网站
date: '2024/2/08 17:00:00'
top_img: 'https://t.mwm.moe/fj'
cover: 'https://t.mwm.moe/fj'
comments: 是否开启评论(true or false)
no_word_count: true <!-- 关闭字数统计 -->
reward: true <!-- 当前文章是否开启打赏 -->
copyright: true <!-- 当前文章是否开启版权声明 -->
categories: 实用技巧
tags:
  - openai
  - ChatGPT
abbrlink: 28011

---

## 搭建背景：

用过 ChatGPT 的朋友都知道，官方网站非常喜欢宕机。
既然如此，那我们就自己搭建一个私信 ChatGPT 服务器吧，直接调用 API 的话，就不担心它会崩溃了。

搭建的方法有很多，以下是参考开源工程项目的搭建方式

## 一、创建 API key

可以搜索 [Open AI](https://openai.com/) 官网，登录到个人 Open AI 账户主页获取你的 API 密钥。

点击 “Create new Secret key” 按钮创建新的密钥，此时会生成新的密钥，然后点击复制按钮先保存一下密钥，后面需要用到（密钥只会显示一次，因此要在第一时间保存好，忘了保存可以再生成一个）。

## 二、注册并登录 GitHub

没有 GitHub 的需要先注册登录，在这就不细说了。

登录 GitHub 之后搜索 “chatgpt-demo”，就可以找到一个镜像 ChatGPT 项目。

## 三、打开项目后往下翻，找到 “Deploy” 按钮，进入 Vercel 页面。

## 四、GitHub 登录 Vercel

进入 Vercel 页面之后选择 GitHub 登录，我这因为之前登陆过，默认登录上了。

接下来填入一个名称，然后点击 “Creat” 按钮

## 五、填入你的 ChatGPT API key

ChatGPT API key 就是前面第一步让大家保存的，然后点击下方的 Deploy 即可。

## 六、等待系统部署

然后点击 visit 或者左下角红框圈出部分即可，到这里我们的 ChatGPT 网站就搭建成功了。