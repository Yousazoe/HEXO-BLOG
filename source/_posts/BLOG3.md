---
title: Hexo-NexT博客使用插件总结
abbrlink: c12c9c40
date: 2021-01-26 17:28:58
tags:
- Hexo
- NexT
- Blog
categories: 博客搭建 (Blog Building)
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/008eGmZEly1gn4nnpskhxj311i0gywkf.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="http://theme-next.iissnan.com/">Hexo NexT</a>
    </i>
  </font>
</div>

### 引言

这几天将博客主题从 Fluid 换回了 NexT，在重新安装插件的时候顺便记录了本博客当前使用的插件以及插件相关的主题美化，便于后续修改和供NexT主题读者参考。

<!--more-->





### 一键部署

#### 地址

- [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)

#### 安装配置

安装插件：

```bash
npm install hexo-deployer-git --save
```

然后修改站点配置文件`_config.yml` 中的配置：

```yaml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
- type: git
  repo:
      github: git@github.com:Yousazoe/yousazoe.github.io.git
      coding: git@e.coding.net:yousazoe/yousazoe/yousazoe.git
  branch: master
```





### 永久链接

#### 地址

- [hexo-abbrlink](https://github.com/rozbo/hexo-abbrlink)

#### 安装配置

安装插件：

```bash
npm install hexo-abbrlink --save
```

然后我们可以在站点配置文件`_config.yml` 中修改为：

```yaml
# URL
## If your site is put in a subdirectory, set url as 'http://example.com/child' and root as '/child/'
url: http://yousazoe.top
root: /
permalink: archives/:abbrlink.html
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32
  rep: hex    # 进制：dec(default) and hex
permalink_defaults:
```





### 文章推荐

这个可以帮助我们根据标签推荐相关文章，原版插件的使用要求编辑主题文件的，但是 NexT 主题集成了这个插件的配置，因此配置起来非常方便。

#### 地址

- [hexo-related-popular-posts](https://github.com/tea3/hexo-related-popular-posts)

#### 安装配置

安装插件：

```bash
npm install hexo-related-popular-posts --save
```

我们只需要在主题配置文件`_config.yml` 中修改：

```yaml
# Related popular posts
# Dependencies: https://github.com/tea3/hexo-related-popular-posts
related_posts:
  enable: ture
  title: # Custom header, leave empty to use the default one
  display_in_home: false
  params:
    maxCount: 5
    #PPMixingRate: 0.0
    #isDate: false
    #isImage: false
    #isExcerpt: false
```



### 站点地图

#### 通用站点地图

- 地址：[hexo-generator-sitemap](https://github.com/hexojs/hexo-generator-sitemap)

安装配置：

```bash
npm install hexo-generator-sitemap --save
```

然后我们需要在 Hexo 站点配置文件`_config.yml` 中加入 sitemap 插件：

```yaml
# 通用站点地图
sitemap:
  path: sitemap.xml
```

#### 百度站点地图

- 地址：[Sitemap generator](https://github.com/coneycode/hexo-generator-baidu-sitemap)

安装配置：

```bash
npm install hexo-generator-baidu-sitemap --save
```

具体配置类似通用站点地图，当然也可以看官方提供的教程，下面是一个简单的配置，我们在 Hexo 站点配置文件`_config.yml` 中添加：

```yaml
# 百度站点地图
baidusitemap:
  path: baidusitemap.xml
```



### 百度推送

#### 地址

- [hexo-baidu-url-submit](https://github.com/huiwang/hexo-baidu-url-submit)

#### 安装配置

安装插件：

```bash
npm install hexo-baidu-url-submit --save
```

在站点配置文件`_config.yml` 中添加以下代码：

```yaml
# 百度主动推送
baidu_url_submit:
  count: 5 				     ## 提交最新的1个链接
  host: tding.top 	     ## 百度站长平台中注册的域名
  token: 	 ## 准入秘钥
  path: baidu_urls.txt 		 ## 文本文档的地址， 新链接会保存在此文本文档里
```



### RSS订阅

#### 地址

+ [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed)



#### 安装配置

```bash
npm install hexo-generator-feed --save
```

在站点的配置根目录`_config.yml`添加：

```yaml
# Extensions
## Plugins: http://hexo.io/plugins/
#RSS订阅
plugin:
- hexo-generator-feed
#Feed Atom
feed:
type: atom
path: atom.xml
limit: 20
```

接着在主题配置文件添加：

```diff
social:
  E-Mail: mailto:zoeyousa@gmail.com || fa fa-envelope
  GitHub: https://github.com/Yousazoe || fab fa-github
  Weibo: https://www.weibo.com/6034231696/profile?rightmod=1&wvr=6&mod=personinfo&is_all=1 || fab fa-weibo
  Steam: https://steamcommunity.com/profiles/76561198856466228/ || fab fa-steam
  Chess: https://www.chess.com/member/yousazoe || fa fa-chess-pawn
+  RSS: /atom.xml || fa fa-rss
```



### 站点统计

#### 地址

+ [hexo-symbols-count-times](https://github.com/theme-next/hexo-symbols-count-time)



#### 安装配置

```bash
npm install hexo-symbols-count-time --save
```

我们只需要在主题配置文件`_config.yml` 中修改：

```yaml
# Post wordcount display settings
# Dependencies: https://github.com/theme-next/hexo-symbols-count-time
symbols_count_time:
  separated_meta: false # 统计信息不换行显示
  item_text_post: false # 文章统计信息中是否显示“本文字数/阅读时长”等描述文字
  item_text_total: ture # 站点统计信息中是否显示“本文字数/阅读时长”等描述文字
  awl: 2 # Average Word Length：平均字符长度
  wpm: 275 # Words Per Minute：阅读速度
```

汉字的平均字符长度为 1.5，如果在文章中使用纯中文进行写作（没有混杂英文），那么推荐设置 `awl: 2` 及 `wpm: 300`，但是如果文章中存在英文，建议设置 `awl: 4` 及 `wpm: 275`。



### 文章置顶

#### 插件配置

```bash
npm uninstall hexo-generator-index --save
npm install hexo-generator-index-pin-top --save
```

#### 图标配置

打开`/themes/next/layout/_macro/` 目录下的`post.swig`文件，在`<div class="post-meta">`的第一个`<span>`标签下，插入如下代码：

```swig
{% if post.top %}
  <i class="fas fa-thumbtack"></i>
  <font color="#C0C0C0">Top</font>
  <span class="post-meta-divider">|</span>
{% endif %}
```







### 站内搜索

#### 地址

+ [hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)



#### 安装配置

```bash
npm install hexo-generator-searchdb --save
```

在**主题配置**文件`themes\next_config.yml`中修改相关字段：

```yaml

local_search:
  enable: true
  trigger: auto # 每次输入改变都执行搜索
  top_n_per_article: 3 # 每篇文章显示的搜索结果数量
  unescape: false
```

在**站点配置**文件`_config.yml`中添加以下字段：

```yaml
search:
  path: search.xml
  field: post # 指定搜索范围，可选 post | page | all
  format: html # 指定页面内容形式，可选 html | raw (Markdown) | excerpt | more
  limit: 10000
```



### 静态资源压缩

#### 地址

+ [hexo-neat](https://github.com/rozbo/hexo-neat)

#### 安装配置

```bash
npm install hexo-neat --save
```

在**站点配置**文件`_config.yml`中添加以下字段：

```yaml
# hexo-neat
# 博文压缩
neat_enable: true
# 压缩html
neat_html:
  enable: true
  exclude:
# 压缩css  
neat_css:
  enable: true
  exclude:
    - '**/*.min.css'
# 压缩js
neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '**/*.min.js'
    - '**/jquery.fancybox.pack.js'
    - '**/index.js'  
```



### 图片懒加载

#### 地址

+ [hexo-lazyload]()

#### 安装配置

```bash
npm install hexo-lazyload --save
```

在**站点配置**文件`_config.yml`中添加以下字段：

```yaml
lazyload:
  enable: true
  # className: #可选 e.g. .J-lazyload-img
  # loadingImg: #可选 eg. ./images/loading.png
```



### 外链优化

减少出站链接能够有效防止权重分散，hexo 有很方便的自动为出站链接添加 `nofollow` 标签的插件。

首先安装 `hexo-filter-nofollow` 插件：

```bash
npm install hexo-filter-nofollow --save
```

然后我们在站点的配置文件`_config.yml` 中添加配置，将 `nofollow` 设置为 `true`：

```yaml
# 外部链接优化
nofollow:
  enable: true
  field: site
  exclude:
    - 'exclude1.com'
    - 'exclude2.com'
```

其中 `exclude`（例外的链接，比如友链）将不会被加上 `nofollow` 属性。



### 侧栏标签云

#### 地址

+ [hexo-tag-cloud](https://github.com/D0n9X1n/hexo-tag-cloud)

#### 安装

- 进入到 hexo 的根目录，然后在 `package.json` 中添加依赖: `"hexo-tag-cloud": "2.1.*"`

- 然后执行 `npm install` 命令

  ```bash
  npm install hexo-tag-cloud
  ```

- 然后需要你去修改主题的 tagcloud 的模板，这个依据你的主题而定。

这里以 Next 主题为例，找到文件 `next/layout/_macro/sidebar.swig`, 然后添加如下内容。

```html
<div class="site-overview-wrap sidebar-panel">
  {{ partial('_partials/sidebar/site-overview.swig', {}, {cache: theme.cache.enable}) }}

  {{- next_inject('sidebar') }}
</div>

{% if site.tags.length > 1 %}
<script type="text/javascript" charset="utf-8" src="{{ url_for('/js/tagcloud.js') }}"></script>
<script type="text/javascript" charset="utf-8" src="{{ url_for('/js/tagcanvas.js') }}"></script>
<div class="widget-wrap">
    <h3 class="widget-title">Tag Cloud</h3>
    <div id="myCanvasContainer" class="widget tagcloud">
        <canvas width="250" height="250" id="resCanvas" style="width:100%">
            {{ list_tags() }}
        </canvas>
    </div>
</div>
{% endif %}

{%- if theme.back2top.enable and theme.back2top.sidebar %}
<div class="back-to-top motion-element">
  <i class="fa fa-arrow-up"></i>
  <span>0%</span>
</div>
{%- endif %}
```



### Live2D

#### 地址

+ [hexo-helper-live2d](https://github.com/EYHN/hexo-helper-live2d)

#### 安装配置

```bash
npm install --save hexo-helper-live2d
```

#### 选择模型

可到https://huaji8.top/post/live2d-plugin-2.0/预览效果。

命令为:`npm install live2d-widget-model-模型名`，模型为可参考上面的预览内容，安装模型:

```bash
npm install live2d-widget-model-hijiki
```



#### 主题配置

站点的配置文件`\_config.yml`或者是主题的配置文件中添加：

```yaml
# Live2D
## https://github.com/EYHN/hexo-helper-live2d
live2d:
  enable: ture
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-hijiki # 模型：https://huaji8.top/post/live2d-plugin-2.0/
  display:
    position: right
    width: 50
    height: 100
  mobile:
    show: true
```



#### 参考

+ [hexo+yilia添加Live2D看板娘](https://yansheng836.github.io/article/e239dc63.html)
+ [hexo live2d插件 2.0 !](https://huaji8.top/post/live2d-plugin-2.0/)



### 播放器标签

#### 地址

+ [hexo-tag-aplayer](https://github.com/MoePlayer/hexo-tag-aplayer)

#### 安装

```bash
npm install hexo-tag-aplayer --save
npm install hexo-tag-dplayer --save
```

#### Aplayer

##### 依赖

- APlayer.js > 1.8.0
- Meting.js > 1.1.1

##### 使用

```markdown
{% aplayer title author url [picture_url, narrow, autoplay, width:xxx, lrc:xxx] %}
```

###### 标签参数

- `title` : 曲目标题
- `author`: 曲目作者
- `url`: 音乐文件 URL 地址
- `picture_url`: (可选) 音乐对应的图片地址
- `narrow`: （可选）播放器袖珍风格
- `autoplay`: (可选) 自动播放，移动端浏览器暂时不支持此功能
- `width:xxx`: (可选) 播放器宽度 (默认: 100%)
- `lrc:xxx`: （可选）歌词文件 URL 地址

当开启 Hexo 的 [文章资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html#文章资源文件夹) 功能时，可以将图片、音乐文件、歌词文件放入与文章对应的资源文件夹中，然后直接引用：

```
{% aplayer "Caffeine" "Jeff Williams" "caffeine.mp3" "picture.jpg" "lrc:caffeine.txt" %}
```

###### 歌词标签

除了使用标签 `lrc` 选项来设定歌词，你也可以直接使用 `aplayerlrc` 标签来直接插入歌词文本在博客中：

```
{% aplayerlrc "title" "author" "url" "autoplay" %}
[00:00.00]lrc here
{% endaplayerlrc %}
```

###### 播放列表

```
{% aplayerlist %}
{
    "narrow": false,                          // （可选）播放器袖珍风格
    "autoplay": true,                         // （可选) 自动播放，移动端浏览器暂时不支持此功能
    "mode": "random",                         // （可选）曲目循环类型，有 'random'（随机播放）, 'single' (单曲播放), 'circulation' (循环播放), 'order' (列表播放)， 默认：'circulation' 
    "showlrc": 3,                             // （可选）歌词显示配置项，可选项有：1,2,3
    "mutex": true,                            // （可选）该选项开启时，如果同页面有其他 aplayer 播放，该播放器会暂停
    "theme": "#e6d0b2",	                      // （可选）播放器风格色彩设置，默认：#b7daff
    "preload": "metadata",                    // （可选）音乐文件预载入模式，可选项： 'none' 'metadata' 'auto', 默认: 'auto'
    "listmaxheight": "513px",                 // (可选) 该播放列表的最大长度
    "music": [
        {
            "title": "CoCo",
            "author": "Jeff Williams",
            "url": "caffeine.mp3",
            "pic": "caffeine.jpeg",
            "lrc": "caffeine.txt"
        },
        {
            "title": "アイロニ",
            "author": "鹿乃",
            "url": "irony.mp3",
            "pic": "irony.jpg"
        }
    ]
}
{% endaplayerlist %}
```

###### MeingJS 支持 (3.0 新功能)

[MetingJS](https://github.com/metowolf/MetingJS) 是基于[Meting API](https://github.com/metowolf/Meting) 的 APlayer 衍生播放器，引入 MetingJS 后，播放器将支持对于 QQ音乐、网易云音乐、虾米、酷狗、百度等平台的音乐播放。

如果想在本插件中使用 MetingJS，请在 Hexo 配置文件 `_config.yml` 中设置：

```yaml
aplayer:
  meting: true
```

接着就可以通过 `{% meting ...%}` 在文章中使用 MetingJS 播放器了：

```
<!-- 简单示例 (id, server, type)  -->
{% meting "60198" "netease" "playlist" %}

<!-- 进阶示例 -->
{% meting "60198" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}
```

有关 `{% meting %}` 的选项列表如下:

| 选项          | 默认值     | 描述                                                        |
| ------------- | ---------- | ----------------------------------------------------------- |
| id            | **必须值** | 歌曲 id / 播放列表 id / 相册 id / 搜索关键字                |
| server        | **必须值** | 音乐平台: `netease`, `tencent`, `kugou`, `xiami`, `baidu`   |
| type          | **必须值** | `song`, `playlist`, `album`, `search`, `artist`             |
| fixed         | `false`    | 开启固定模式                                                |
| mini          | `false`    | 开启迷你模式                                                |
| loop          | `all`      | 列表循环模式：`all`, `one`,`none`                           |
| order         | `list`     | 列表播放模式： `list`, `random`                             |
| volume        | 0.7        | 播放器音量                                                  |
| lrctype       | 0          | 歌词格式类型                                                |
| listfolded    | `false`    | 指定音乐播放列表是否折叠                                    |
| storagename   | `metingjs` | LocalStorage 中存储播放器设定的键名                         |
| autoplay      | `true`     | 自动播放，移动端浏览器暂时不支持此功能                      |
| mutex         | `true`     | 该选项开启时，如果同页面有其他 aplayer 播放，该播放器会暂停 |
| listmaxheight | `340px`    | 播放列表的最大长度                                          |
| preload       | `auto`     | 音乐文件预载入模式，可选项： `none`, `metadata`, `auto`     |
| theme         | `#ad7a86`  | 播放器风格色彩设置                                          |

关于如何设置自建的 Meting API 服务器地址，以及其他 MetingJS 配置，请参考章节[自定义配置](https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md#自定义配置30-新功能)

###### PJAX 兼容

若在 Hexo 中使用了 PJAX，可能需要自己手动清理 APlayer 全局实例：

```
$(document).on('pjax:start', function () {
    if (window.aplayers) {
        for (let i = 0; i < window.aplayers.length; i++) {
            window.aplayers[i].destroy();
        }
        window.aplayers = [];
    }
});
```

##### 自定义配置（3.0 新功能）

现在你可以在 Hexo 配置文件 `_config.yml` 中配置本插件：

```yaml
aplayer:
  script_dir: some/place                        # Public 目录下脚本目录路径，默认: 'assets/js'
  style_dir: some/place                         # Public 目录下样式目录路径，默认: 'assets/css'
  cdn: http://xxx/aplayer.min.js                # 引用 APlayer.js 外部 CDN 地址 (默认不开启)
  style_cdn: http://xxx/aplayer.min.css         # 引用 APlayer.css 外部 CDN 地址 (默认不开启)
  meting: true                                  # MetingJS 支持
  meting_api: http://xxx/api.php                # 自定义 Meting API 地址
  meting_cdn: http://xxx/Meing.min.js           # 引用 Meting.js 外部 CDN 地址 (默认不开启)
  asset_inject: true                            # 自动插入 Aplayer.js 与 Meting.js 资源脚本, 默认开启
  externalLink: http://xxx/aplayer.min.js       # 老版本参数，功能与参数 cdn 相同
```



#### Dplayer

##### 快速开始

我们先尝试初始化一个最简单的 DPlayer

加载播放器文件:

```html
<div id="dplayer"></div>
<script src="DPlayer.min.js"></script>
```

或者使用模块管理器:

```js
import DPlayer from 'dplayer';

const dp = new DPlayer(options);
```

在 js 里初始化:

```js
const dp = new DPlayer({
    container: document.getElementById('dplayer'),
    video: {
        url: 'demo.mp4',
    },
});
```

一个最简单的 DPlayer 就初始化好了，它只有最基本的视频播放功能

##### 参数

DPlayer 有丰富的参数可以自定义你的播放器实例

| 名称                 | 默认值                             | 描述                                                         |
| -------------------- | ---------------------------------- | ------------------------------------------------------------ |
| container            | document.querySelector('.dplayer') | 播放器容器元素                                               |
| live                 | false                              | 开启直播模式, 见[#直播](http://dplayer.js.org/zh/guide.html#直播) |
| autoplay             | false                              | 视频自动播放                                                 |
| theme                | '#b7daff'                          | 主题色                                                       |
| loop                 | false                              | 视频循环播放                                                 |
| lang                 | navigator.language.toLowerCase()   | 可选值: 'en', 'zh-cn', 'zh-tw'                               |
| screenshot           | false                              | 开启截图，如果开启，视频和视频封面需要允许跨域               |
| hotkey               | true                               | 开启热键，支持快进、快退、音量控制、播放暂停                 |
| airplay              | true                               | 在 Safari 中开启 AirPlay                                     |
| preload              | 'auto'                             | 视频预加载，可选值: 'none', 'metadata', 'auto'               |
| volume               | 0.7                                | 默认音量，请注意播放器会记忆用户设置，用户手动设置音量后默认音量即失效 |
| playbackSpeed        | [0.5, 0.75, 1, 1.25, 1.5, 2]       | 可选的播放速率，可以设置成自定义的数组                       |
| logo                 | -                                  | 在左上角展示一个 logo，你可以通过 CSS 调整它的大小和位置     |
| apiBackend           | -                                  | 自定义获取和发送弹幕行为，见[#直播](http://dplayer.js.org/zh/guide.html#直播) |
| video                | -                                  | 视频信息                                                     |
| video.quality        | -                                  | 见[#清晰度切换](http://dplayer.js.org/zh/guide.html#清晰度切换) |
| video.defaultQuality | -                                  | 见[#清晰度切换](http://dplayer.js.org/zh/guide.html#清晰度切换) |
| video.url            | -                                  | 视频链接                                                     |
| video.pic            | -                                  | 视频封面                                                     |
| video.thumbnails     | -                                  | 视频缩略图，可以使用 [DPlayer-thumbnails (opens new window)](https://github.com/MoePlayer/DPlayer-thumbnails)生成 |
| video.type           | 'auto'                             | 可选值: 'auto', 'hls', 'flv', 'dash', 'webtorrent', 'normal' 或其他自定义类型, 见[#MSE 支持](http://dplayer.js.org/zh/guide.html#mse-支持) |
| video.customType     | -                                  | 自定义类型, 见[#MSE 支持](http://dplayer.js.org/zh/guide.html#mse-支持) |
| subtitle             | -                                  | 外挂字幕                                                     |
| subtitle.url         | `required`                         | 字幕链接                                                     |
| subtitle.type        | 'webvtt'                           | 字幕类型，可选值: 'webvtt', 'ass'，目前只支持 webvtt         |
| subtitle.fontSize    | '20px'                             | 字幕字号                                                     |
| subtitle.bottom      | '40px'                             | 字幕距离播放器底部的距离，取值形如: '10px' '10%'             |
| subtitle.color       | '#fff'                             | 字幕颜色                                                     |
| danmaku              | -                                  | 显示弹幕                                                     |
| danmaku.id           | `required`                         | 弹幕池 id，必须唯一                                          |
| danmaku.api          | `required`                         | 见[#弹幕接口](http://dplayer.js.org/zh/guide.html#弹幕接口)  |
| danmaku.token        | -                                  | 弹幕后端验证 token                                           |
| danmaku.maximum      | -                                  | 弹幕最大数量                                                 |
| danmaku.addition     | -                                  | 额外外挂弹幕，见[#bilibili 弹幕](http://dplayer.js.org/zh/guide.html#bilibili-弹幕) |
| danmaku.user         | 'DIYgod'                           | 弹幕用户名                                                   |
| danmaku.bottom       | -                                  | 弹幕距离播放器底部的距离，防止遮挡字幕，取值形如: '10px' '10%' |
| danmaku.unlimited    | false                              | 海量弹幕模式，即使重叠也展示全部弹幕，请注意播放器会记忆用户设置，用户手动设置后即失效 |
| contextmenu          | []                                 | 自定义右键菜单                                               |
| highlight            | []                                 | 自定义进度条提示点                                           |
| mutex                | true                               | 互斥，阻止多个播放器同时播放，当前播放器播放时暂停其他播放器 |

```js
const dp = new DPlayer({
    container: document.getElementById('dplayer'),
    autoplay: false,
    theme: '#FADFA3',
    loop: true,
    lang: 'zh-cn',
    screenshot: true,
    hotkey: true,
    preload: 'auto',
    logo: 'logo.png',
    volume: 0.7,
    mutex: true,
    video: {
        url: 'dplayer.mp4',
        pic: 'dplayer.png',
        thumbnails: 'thumbnails.jpg',
        type: 'auto',
    },
    subtitle: {
        url: 'dplayer.vtt',
        type: 'webvtt',
        fontSize: '25px',
        bottom: '10%',
        color: '#b7daff',
    },
    danmaku: {
        id: '9E2E3368B56CDBB4',
        api: 'https://api.prprpr.me/dplayer/',
        token: 'tokendemo',
        maximum: 1000,
        addition: ['https://api.prprpr.me/dplayer/v3/bilibili?aid=4157142'],
        user: 'DIYgod',
        bottom: '15%',
        unlimited: true,
    },
    contextmenu: [
        {
            text: 'custom1',
            link: 'https://github.com/DIYgod/DPlayer',
        },
        {
            text: 'custom2',
            click: (player) => {
                console.log(player);
            },
        },
    ],
    highlight: [
        {
            time: 20,
            text: '这是第 20 秒',
        },
        {
            time: 120,
            text: '这是 2 分钟',
        },
    ],
});
```

##### API

- `dp.play()`: 播放视频

- `dp.pause()`: 暂停视频

- `dp.seek(time: number)`: 跳转到特定时间

  ```js
  dp.seek(100);
  ```

- `dp.toggle()`: 切换播放和暂停

- `dp.on(event: string, handler: function)`: 绑定视频和播放器事件，见[#事件绑定](http://dplayer.js.org/zh/guide.html#事件绑定)

- `dp.switchVideo(video, danmaku)`: 切换到其他视频

  ```js
  dp.switchVideo(
      {
          url: 'second.mp4',
          pic: 'second.png',
          thumbnails: 'second.jpg',
      },
      {
          id: 'test',
          api: 'https://api.prprpr.me/dplayer/',
          maximum: 3000,
          user: 'DIYgod',
      }
  );
  ```

- `dp.notice(text: string, time: number)`: 显示通知，时间的单位为毫秒，默认时间 2000 毫秒，默认透明度 0.8

- `dp.switchQuality(index: number)`: 切换清晰度

- `dp.destroy()`: 销毁播放器

- `dp.speed(rate: number)`: 设置视频速度

- `dp.volume(percentage: number, nostorage: boolean, nonotice: boolean)`: 设置视频音量

  ```js
  dp.volume(0.1, true, false);
  ```

- `dp.video`: 原生 video

- `dp.video.currentTime`: 返回视频当前播放时间

- `dp.video.duration`: 返回视频总时间

- `dp.video.paused`: 返回视频是否暂停

- 支持大多数[原生 video 接口(opens new window)](http://www.w3schools.com/tags/ref_av_dom.asp)

- `dp.danmaku`

- `dp.danmaku.send(danmaku, callback: function)`: 提交一个新弹幕

  ```js
  dp.danmaku.send(
      {
          text: 'dplayer is amazing',
          color: '#b7daff',
          type: 'right', // should be `top` `bottom` or `right`
      },
      function () {
          console.log('success');
      }
  );
  ```

- `dp.danmaku.draw(danmaku)`: 实时绘制一个新弹幕

  ```js
  dp.danmaku.draw({
      text: 'DIYgod is amazing',
      color: '#fff',
      type: 'top',
  });
  ```

- `dp.danmaku.opacity(percentage: number)`: 设置弹幕透明度，透明度值在 0 到 1 之间

  ```js
  dp.danmaku.opacity(0.5);
  ```

- `dp.danmaku.clear()`: 清除所有弹幕

- `dp.danmaku.hide()`: 隐藏弹幕

- `dp.danmaku.show()`: 显示弹幕

- `dp.fullScreen`: 两个类型：`web` 和 `browser`，默认类型是 `browser`

- `dp.fullScreen.request(type: string)`: 进入全屏

  ```js
  dp.fullScreen.request('web');
  ```

- `dp.fullScreen.cancel(type: string)`: 退出全屏

  ```js
  dp.fullScreen.cancel('web');
  ```

##### 事件绑定

```javascript
dp.on(event, handler)
dp.on('ended', function () {
    console.log('player ended');
});
```

视频事件

- abort
- canplay
- canplaythrough
- durationchange
- emptied
- ended
- error
- loadeddata
- loadedmetadata
- loadstart
- mozaudioavailable
- pause
- play
- playing
- progress
- ratechange
- seeked
- seeking
- stalled
- suspend
- timeupdate
- volumechange
- waiting

播放器事件

- screenshot
- thumbnails_show
- thumbnails_hide
- danmaku_show
- danmaku_hide
- danmaku_clear
- danmaku_loaded
- danmaku_send
- danmaku_opacity
- contextmenu_show
- contextmenu_hide
- notice_show
- notice_hide
- quality_start
- quality_end
- destroy
- resize
- fullscreen
- fullscreen_cancel
- subtitle_show
- subtitle_hide
- subtitle_change

##### 清晰度切换

在 `video.quality` 里设置不同清晰度的视频链接和类型，`video.defaultQuality` 设置默认清晰度

Load demo

```js
const dp = new DPlayer({
    container: document.getElementById('dplayer'),
    video: {
        quality: [
            {
                name: 'HD',
                url: 'demo.m3u8',
                type: 'hls',
            },
            {
                name: 'SD',
                url: 'demo.mp4',
                type: 'normal',
            },
        ],
        defaultQuality: 0,
        pic: 'demo.png',
        thumbnails: 'thumbnails.jpg',
    },
});
```

##### 弹幕

###### 弹幕接口

```
danmaku.api
```

**现成的接口**

链接: https://api.prprpr.me/dplayer/

每日备份: [DPlayer-data(opens new window)](https://github.com/DIYgod/DPlayer-data)

**自己搭建**

[DPlayer-node(opens new window)](https://github.com/MoePlayer/DPlayer-node)

###### bilibili 弹幕

```
danmaku.addition
```

API: [https://api.prprpr.me/dplayer/v3/bilibili?aid=[aid](opens new window)](https://api.prprpr.me/dplayer/v3/bilibili?aid=[aid])

```js
const option = {
    danmaku: {
        // ...
        addition: ['https://api.prprpr.me/dplayer/v3/bilibili?aid=[aid]'],
    },
};
```