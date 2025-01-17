---
title: Hexo Butterfly主题美化
date: '2023/12/31 22:00:00'
top_img: 'https://t.mwm.moe/fj'
cover: 'https://t.mwm.moe/fj'
comments: 是否开启评论(true or false)
no_word_count: true <!-- 关闭字数统计 -->
reward: true <!-- 当前文章是否开启打赏 -->
copyright: true <!-- 当前文章是否开启版权声明 -->
categories: 实用技巧
tags:
  - hexo、GitHub、Butterfly
abbrlink: 28011
---

## 代码样式

> 代码块中的所有功能只适用于 Hexo 自带的代码渲染。如果使用第三方的渲染器，不一定会有效

### 代码高亮主题

`Butterfly` 支持 6 种代码高亮样式：

- darker
- pale night
- light
- ocean
- mac
- mac light

修改主题配置文件 `_config.butterfly.yml`

```yaml
highlight_theme: mac
```

### 代码复制

主题支持代码复製功能

修改 主题配置文件

```yaml
highlight_copy: true
```

### 代码高度限制

> 3.7.0 及以上支持

## 顶部图

| 配置             | 解释                                                         |
| ---------------- | ------------------------------------------------------------ |
| index_img        | 主页的 top_img                                               |
| default_top_img  | 默认的 top_img，当页面的 top_img 没有配置时，会显示 default_top_img |
| archive_img      | 归档页面的 top_img                                           |
| tag_img          | tag 子页面 的 默认 top_img                                   |
| tag_per_img      | tag 子页面的 top_img，可配置每个 tag 的 top_img              |
| category_img     | category 子页面 的 默认 top_img                              |
| category_per_img | category 子页面的 top_img，可配置每个 category 的 top_img    |

修改主题配置文件 `_config.butterfly.yml`

```yaml
index_img: xxx.png
```

其它页面 （tags/categories/ 自建页面）和文章页的 `top_img` ，请到对应的 md 页面设置 `front-matter` 中的 `top_img`

`tag_per_img` 和 `category_per_img` 是 3.2.0 新增的内容，可对 tag 和 category 进行单独的配置

并不推荐为每个 tag 和每个 category 都配置不同的顶部图，因为配置太多会拖慢生成速度

```yaml
tag_per_img：
  aplayer: https://xxxxxx.png
  android: ddddddd.png

category_per_img：
  随想: hdhdh.png
  推荐: ddjdjdjd.png
```

## footer 背景

修改主题配置文件 `_config.butterfly.yml`

```yaml
# footer是否显示图片背景(与 top_img一致)
footer_bg: true
```

## 打字效果

打字效果 [activate-power-mode](https://github.com/disjukr/activate-power-mode)

修改主题配置文件 `_config.butterfly.yml`

```yaml
# Typewriter Effect (打字效果)
# https://github.com/disjukr/activate-power-mode
activate_power_mode:
  enable: true
  colorful: true # open particle animation (冒光特效)
  shake: true #  open shake (抖動特效)
  mobile: false
```

## 鼠标点击效果

`zIndex` 建议只在 `-1` 和 `9999` 上选
`-1` 代表烟火效果在底部
`9999` 代表烟火效果在前面

修改主题配置文件 `_config.butterfly.yml`

```yaml
fireworks:
  enable: true
  zIndex: 9999 # -1 or 9999
  mobile: false
```

## 网站副标题

可设置主页中展示的网站副标题或者自己喜欢的座右铭

修改主题配置文件 `_config.butterfly.yml`

```yaml
# Site
title: Hexo
subtitle:
  enable: true
  # Typewriter Effect (打字效果)
  effect: true
  # loop (循環打字)
  loop: true
  # source 調用第三方服務
  # source: false 關閉調用
  # source: 1  調用一言網的一句話（簡體） https://hitokoto.cn/
  # source: 2  調用一句網（簡體） http://yijuzhan.com/
  # source: 3  調用今日詩詞（簡體） https://www.jinrishici.com/
  # subtitle 會先顯示 source , 再顯示 sub 的內容
  # source: 3
  # 如果關閉打字效果，subtitle 只會顯示 sub 的第一行文字
  sub:
    - xxxxx
    - xxxxx
    - xxxxx
```

## 侧边栏设置

### 侧边排版

可自行决定哪个项目需要显示，可决定位置，也可以设置不显示侧边栏。

Butterfly支持 [font-awesome v6](https://fontawesome.com/icons?from=io)圖標.

修改主题配置文件 `_config.butterfly.yml`

```yaml
aside:
  enable: true
  hide: false
  button: true
  mobile: false # display on mobile
  position: right # left or right
  card_author:
    enable: true
    description: 手握日月摘心陈
    button:
      enable: true
      icon: iconfont icon-youxishoubing
      text: 摸鱼
      link: https://zmswa.cn/
  card_announcement:
    enable: true
    content:
      <b><font color="#e66b6d">双</font> <font color="#e66d98">手</font> <font color="#e66cc6">合</font> <font color="#cc6de6">十</font> <font color="#9770e6">成</font> <font color="#6d93e6">为</font> <font color="#6fcde6">自</font> <font color="#72e6b6">己</font> <font color="#72e689">的</font> <font color="#99e670">神</font>, <font color="#cde670">自</font> <font color="#e6df72">己</font> <font color="#e6c073">所</font> <font color="#e6a271">信</font> <font color="#e6796f">念</font> <font color="#e65454">的</font> <font color="#e63333">即</font> <font color="#e62c2c">是</font> <font color="#e60101">信</font> <font color="#e60101">仰</font></b>
      <p align="center"><img src="https://haiyong.site/img/img-blog.csdnimg.cn/f7384c88956d4378b72e47548e19c9f8.gif" width="50" alt="mao"></p>
      <p align="center">微信号：  </p>
      <p align="center">QQ号：491298200</p>
  card_recent_post:
    enable: true
    limit: 5 # if set 0 will show all
    sort: date # date or updated
    sort_order: # Don't modify the setting unless you know how it works
  card_categories:
    enable: true
    limit: 8 # if set 0 will show all
    expand: none # none/true/false
    sort_order: # Don't modify the setting unless you know how it works
  card_tags:
    enable: true
    limit: 40 # if set 0 will show all
    color: true
    sort_order: # Don't modify the setting unless you know how it works
  card_archives:
    enable: true
    type: monthly # yearly or monthly
    format: MMMM YYYY # eg: YYYY年MM月
    order: -1 # Sort of order. 1, asc for ascending; -1, desc for descending
    limit: 8 # if set 0 will show all
    sort_order: # Don't modify the setting unless you know how it works
  card_webinfo:
    enable: true
    post_count: true
    last_push_date: true
    sort_order: # Don't modify the setting unless you know how it works
  card_tags color: true
```

### 访问人数 busuanzi (UV 和 PV)

访问 busuanzi 的[官方网站](http://busuanzi.ibruce.info/)查看更多的介绍。

修改主题配置文件 `_config.butterfly.yml`

```yaml
busuanzi:
  site_uv: true
  site_pv: true
  page_pv: true
```



### 运行时间

网页已运行时间

修改主题配置文件 `_config.butterfly.yml`

```yaml
runtimeshow:
  enable: true
  publish_date: 6/7/2018 00:00:00  
  ##网页开通时间
  #格式: 月/日/年 时间
  #也可以写成 年/月/日 时间
```

## 侧边栏时钟 （转载自：[安知鱼](https://anzhiy.cn/posts/fc18.html)）

1、如果有安装店长的插件版侧边栏电子钟（与店长的电子钟冲突），在博客根目录 [Blogroot] 下打开终端，运行以下指令

```bash
# 卸载原版电子钟
npm uninstall hexo-butterfly-clock
```

2、安装插件，在博客根目录 `[Blogroot]` 下打开终端，运行以下指令：

```bash
npm install hexo-butterfly-clock-anzhiyu --save
```

3、添加配置信息，以下为写法示例在站点配置文件`_config.yml` 或者主题配置文件`_config.butterfly.yml` 中添加

```yaml
# electric_clock
# see https://anzhiy.cn/posts/fc18.html
electric_clock:
  enable: true # 开关
  priority: 5 #过滤器优先权
  enable_page: all # 应用页面
  exclude:
  # - /posts/
  # - /about/
  layout: # 挂载容器类型
    type: class
    name: sticky_layout
    index: 0
  loading: https://cdn.cbd.int/hexo-butterfly-clock-anzhiyu/lib/loading.gif #加载动画自定义
  clock_css: https://cdn.cbd.int/hexo-butterfly-clock-anzhiyu/lib/clock.min.css
  clock_js: https://cdn.cbd.int/hexo-butterfly-clock-anzhiyu/lib/clock.min.js
  ip_api: https://widget.qweather.net/simple/static/js/he-simple-common.js?v=2.0
  qweather_key: # 和风天气key
  gaud_map_key: # 高得地图web服务key
  default_rectangle: false # 开启后将一直显示rectangle位置的天气，否则将获取访问者的地理位置与天气
  rectangle: 112.982279,28.19409 # 获取访问者位置失败时会显示该位置的天气，同时该位置为开启default_rectangle后的位置
```

其中 `qweather_key` 和 `gaud_map_key` 最好自己去申请对应的 api key，默认使用安知鱼的，可能会被限制，不保证可靠性

## 字数统计

要为 Butterfly 配上字数统计特性，你需要如下几个步骤:

1. 打开 hexo 工作目录
2. npm install hexo-wordcount —save or yarn add hexo-wordcount
3. 修改主题配置文件 `_config.butterfly.yml`

```yaml
wordcount:
  enable: true
  post_wordcount: true
  min2read: true
  total_wordcount: true
```

### 动态标题

如我网站所示，当你离开本站，标签页会显示 `w(ﾟДﾟ)w 不要走！再看看嘛！`，回到本站显示`♪(^∇^*)欢迎回来！`，如何实现此效果？

其实很简单，在你的 JS 中加入以下代码即可：

```javascript
//动态标题
var OriginTitile = document.title;
var titleTime;
document.addEventListener('visibilitychange', function () {
    if (document.hidden) {
        //离开当前页面时标签显示内容
        document.title = 'w(ﾟДﾟ)w 不要走！再看看嘛！';
        clearTimeout(titleTime);
    }
    else {
        //返回当前页面时标签显示内容
        document.title = '♪(^∇^*)欢迎回来！' + OriginTitile;
        //两秒后变回正常标题
        titleTime = setTimeout(function () {
            document.title = OriginTitile;
        }, 2000);
    }
});
```

## 公告 2 个小人

1、在 `Butterfly/layout/includes/widget/card_announcement.pug` 下添加如下代码：

```javascript

 .xpand(style='height:200px;')
  canvas.illo(width='800' height='800' style='max-width: 200px; max-height: 200px; touch-action: none; width: 640px; height: 640px;')
script(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/twopeople1.js')
script(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/zdog.dist.js')
script#rendered-js(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/twopeople.js')
style.
  .card-widget.card-announcement {
  margin: 0;
  align-items: center;
  justify-content: center;
  text-align: center;
  }
  canvas {
  display: block;
  margin: 0 auto;
  cursor: move;
  }
```

## 引入 Aplayer 播放音乐

1、在博客根目录 `[Blogroot]` 下打开终端，运行以下指令安装 [hexo-tag-aplayer](https://www.npmjs.com/package/hexo-tag-aplayer) 插件：

```bash
npm install hexo-tag-aplayer --save
```

2、在站点配置文件 `[Blogroot]\_config.yml` 中新增配置项，建议直接加在最底下：

```yml
# APlayer
# https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md
aplayer:
  meting: true
  asset_inject: false
```

3、修改主题配置文件 `[Blogroot]\_config.butterfly.yml` 中关于 Aplayer 的配置内容：

```yaml
# Inject the css and script (aplayer/meting)
aplayerInject:
  enable: true
  per_page: true
```

4、在主题配置文件 `[Blogroot]\_config.butterfly.yml` 的 inject 配置项中添加 Aplayer 的容器。

```yaml
inject:
  head:
  bottom:
    - <div class="aplayer no-destroy" data-id="5183531430" data-server="netease" data-type="playlist" data-fixed="true" data-mini="true" data-listFolded="false" data-order="random" data-preload="none" data-autoplay="false" muted></div>
```

5、在博客根目录 `[Blogroot]` 下打开终端，运行以下指令：

```
hexo clean
hexo generate
hexo server
```

6、关于更换歌单的问题，大部分同学都因为只更改了 data-id 的值，所以出现歌单加载不出的情况，此处需要注意，**data-id**、**data-server**、**data-type** 分别对应了`歌单的id，歌单的服务商、歌单的类型`~~（感觉自己说了废话）~~，所以需要确认这三项是一一对应的。

7、Aplayer 的网易云歌单接口时不时的会挂掉，所以如果你确定你配置正确，但是歌单还是没有出现。不妨去看看其他人的站点是不是也没有 Aplayer 标签了来判断是 Aplayer 本身接口的问题还是自己配置出错的问题。

8、配置成功后会发现 Aplayer 的吸底标签一直占据着左下角的一片空间，对手机端阅读不太友好，可以添加一下 CSS 样式使其自动缩进隐藏。在 `[Blogroot]\themes\butterfly\source\css\custom.css` 中 (没有这个文件就按照路径自己新建) 添加如下内容：

```css

.aplayer.aplayer-fixed.aplayer-narrow .aplayer-body {
  left: -66px !important;
  /* 默认情况下缩进左侧66px，只留一点箭头部分 */
}

.aplayer.aplayer-fixed.aplayer-narrow .aplayer-body:hover {
  left: 0 !important;
  /* 鼠标悬停是左侧缩进归零，完全显示按钮 */
}
```

9、不要忘了到主题配置文件引入自定义样式，修改 `[Blogroot]_config.butterfly.yml` 的 `inject` 配置项：

```diff
  inject:
    head:
+     - <link rel="stylesheet" href="/css/custom.css"  media="defer" onload="this.media='all'">
    bottom:
      - <div class="aplayer no-destroy" data-id="5183531430" data-server="netease" data-type="playlist" data-fixed="true" data-mini="true" data-listFolded="false" data-order="random" data-preload="none" data-autoplay="false" muted></div>
```

