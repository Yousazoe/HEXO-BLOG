---
title: 博客使用插件总结
abbrlink: c12c9c40
date: 2021-01-26 17:28:58
tags:
  - Hexo
  - NexT
  - Blog
categories:
  - 博客搭建 (Blog Building)
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

+ []()

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

[hexo-tag-cloud](https://github.com/D0n9X1n/hexo-tag-cloud)

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



