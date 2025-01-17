---
title: CNAME解析至cf：分流解析cloudflare处理国外请求
date: '2024/02/02 22:00:00'
top_img: 'https://t.mwm.moe/fj'
cover: 'https://t.mwm.moe/fj'
comments: 是否开启评论(true or false)
no_word_count: true <!-- 关闭字数统计 -->
reward: true <!-- 当前文章是否开启打赏 -->
copyright: true <!-- 当前文章是否开启版权声明 -->
categories: 实用技巧
tags:
  - Cloudflare
abbrlink: 28011

---

域名接入cloudflare
此处不再赘述如何创建cloudflare账号，在cloudflare官网创建好账号后

登录 => 主页 => 添加网站
![添加网站](https://img02.anheyu.com/adminuploads/1/2023/07/23/64bd0c9d6d6b3.webp!blogimg)

输入你的域名


选择Free计划
![选择Free计划](https://img02.anheyu.com/adminuploads/1/2023/07/23/64bd0d426c037.png!blogimg)

cloudflare会扫描已有DNS记录，将已有的DNS记录添加进去，这一步很重要，防止出现服务中断，如果这一步没做好，可能会有部分站点后面没有解析导致出现网站不可访问的现象，将所有已经有的解析记录都在这一步加好。

![Image 6 of 12](https://img02.anheyu.com/adminuploads/1/2023/07/23/64bd0d8187168.png!blogimg)

获取到cloudflare到NS服务器地址

![Image 7 of 12](https://img02.anheyu.com/adminuploads/1/2023/07/23/64bd0e56a1fb3.png!blogimg)


登录你的域名厂商解析修改域名的DNS服务器，此处以腾讯云举例
打开 域名控制台 点击修改DNS服务器地址



添加上刚刚在cloudflare获取到的DNS服务器地址，两个都加上，此时只是暂时改，为了通过✅cloudflare的监测，通过以后就可以改回来了。



等待⌛️10分钟左右，cloudflare会发送一封邮件📧 说明DNS服务器修改成功，改成功以后就可以正式开始接入了，在左侧的DNS->记录可以找到你的所有记录，在这里可以把你的解析记录都加好，解析到你的服务器上，并且打开代理状态的小云朵☁️，亮起则代表，cloudflare正在代理你的流量，才能起到防护作用，否则只有解析作用。

8. 左侧的DNS->记录中，最下面可以看到一开始你验证的时候的NS值，将这个NS值复制下来，然后到腾讯云进行境外解析，添加NS记录，记得需要两条，这样一个域名，在腾讯云就有三条解析记录，在cloudflare有一条。


最后再在腾讯云将DNS服务器改回来dnspod


就可以达到境内解析为国内CDN，境外解析为cloudflare防护。

总结
弊端1：不适用于根域名，只能子域名（二级域名等）使用NS解析过去
弊端2：依赖于dnspod的解析ip池判断，某些地区可能存在判断错误（移动尤为明显）

优势：免费的要什么自行车

总的来说还是很不错的，值得一试，另外也可以将境外的解析到奇安信CDN上，也能达到类似的效果。

来自 [安知鱼](https://blog.anheyu.com/)！

