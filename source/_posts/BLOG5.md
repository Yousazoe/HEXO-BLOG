---
title: Hexo-NexT博客问题汇总
comment: false
abbrlink: cea8188d
date: 2021-03-07 16:38:22
type:
tags:
- Hexo
- NexT
- Blog
categories: 博客搭建 (Blog Building)
banner_img:
index_img:
translate_title:
top:
mathjax:
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0b6de466763819.5b47a374e8c64.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/66763819/Why-Use-Fleet-Maintenance-Software?tracking_source=for_you_feed_featured_category">Why Use Fleet Maintenance Software</a> by 
      <a href="https://www.behance.net/ucwang">Yu Shin Wang</a>
    </i>
  </font>
</div>



### 引言

本文对Hexo博客+NexT主题使用中出现的各种问题进行总结，方便读者解决这些遇到的相同问题。

<!--more-->





### 标签云回滚

#### 问题描述

在部分页面在下拉过程会出现回滚情况，导致无法到达底部。最开始是在标签页发现的，几次测试还具有一定的随机性，在Chrome上。在手机端因为不显示sidebar所以没有这个问题。



#### 解决方案

注释掉标签云：

```diff
-      {% if site.tags.length > 1 %}
-      <script type="text/javascript" charset="utf-8" src="{{ url_for('/js/tagcloud.js') }}"></script>
-      <script type="text/javascript" charset="utf-8" src="{{ url_for('/js/tagcanvas.js') }}"></script>
-      <div class="widget-wrap">
-          <h5 class="widget-title"></h5>
-          <div id="myCanvasContainer" class="widget tagcloud">
-              <canvas width="250" height="250" id="resCanvas" style="width:100%">
-                  {{ list_tags() }}
-              </canvas>
-          </div>
-      </div>
-      {% endif %}
```







### pjax刷新

#### 问题描述

在使用音乐播放器Aplayer与说说Artitalk时发现必须刷新两次才能加载出来。



#### 解决方案

最开始尝试在这几个页面不使用pjax：

```yaml
pjax: ture  
  exclude: 
  	- '/about/'
  	- '/artitalk/'
```

但问题并没有解决，第一次刷新还是什么也没有，需要再次刷新才显示内容。

目前没有两全其美的办法，对于页面间跳转我的需求并不是很高，所以在主题配置文件中关闭了pjax选项，音乐播放器与Artitalk均恢复正常。

```yaml
# Easily enable fast Ajax navigation on your website.
# Dependencies: https://github.com/theme-next/theme-next-pjax
- pjax: ture
+ pjax: false
```



后面加入Artitalk的交流群询问是否兼容pjax，得到的答案是不行。在关闭pjax后页面间跳转明显变慢，后面又查询了一下找到一种折中的办法：pjax页面刷新两次。在`themes/layout/pjax.swig`中加入刷新代码：

```diff
<script>
var pjax = new Pjax({
  selectors: [
    'head title',
    '#page-configurations',
    '.content-wrap',
    '.post-toc-wrap',
    '.languages',
    '#pjax'
  ],
  switches: {
    '.post-toc-wrap': Pjax.switches.innerHTML
  },
  analytics: false,
  cacheBust: false,
  scrollTo : !CONFIG.bookmark.enable
});

window.addEventListener('pjax:success', () => {
  document.querySelectorAll('script[data-pjax], script#page-configurations, #pjax script').forEach(element => {
    var code = element.text || element.textContent || element.innerHTML || '';
    var parent = element.parentNode;
    parent.removeChild(element);
    var script = document.createElement('script');
    if (element.id) {
      script.id = element.id;
    }
    if (element.className) {
      script.className = element.className;
    }
    if (element.type) {
      script.type = element.type;
    }
    if (element.src) {
      script.src = element.src;
      // Force synchronous loading of peripheral JS.
      script.async = false;
    }
    if (element.dataset.pjax !== undefined) {
      script.dataset.pjax = '';
    }
    if (code !== '') {
      script.appendChild(document.createTextNode(code));
    }
    parent.appendChild(script);
  });

  
  NexT.boot.refresh();
+ loadMeting();
  // Define Motion Sequence & Bootstrap Motion.
  if (CONFIG.motion.enable) {
    NexT.motion.integrator
      .init()
      .add(NexT.motion.middleWares.subMenu)
      .add(NexT.motion.middleWares.postList)
      .bootstrap();
  }
  
  
  NexT.utils.updateSidebarPosition();

+ $(document).ready(function () {
+     if(location.href.indexOf("#reloaded")==-1){
+         location.href=location.href+"#reloaded";
+         location.reload();
+     }
+ }）

});
</script>

```



这样从某种程度保证了性能和花里胡哨，但刷新也无形中降低了性能，所以是把双刃剑取舍由读者来选择。但如果我们简单掉换一下顺序，在开头就重新刷新就没必要全部渲染完后再重新加载，性能提升了许多：

```diff
<script>
var pjax = new Pjax({
  selectors: [
    'head title',
    '#page-configurations',
    '.content-wrap',
    '.post-toc-wrap',
    '.languages',
    '#pjax'
  ],
  switches: {
    '.post-toc-wrap': Pjax.switches.innerHTML
  },
  analytics: false,
  cacheBust: false,
  scrollTo : !CONFIG.bookmark.enable
});

window.addEventListener('pjax:success', () => {
+    $(document).ready(function () {

+    if(location.href.indexOf("#reloaded")==-1){
+        location.href=location.href+"#reloaded";
+        location.reload();
+    }
+}）
#在这后面可以加入程序的其他代码  


  document.querySelectorAll('script[data-pjax], script#page-configurations, #pjax script').forEach(element => {
    var code = element.text || element.textContent || element.innerHTML || '';
    var parent = element.parentNode;
    parent.removeChild(element);
    var script = document.createElement('script');
    if (element.id) {
      script.id = element.id;
    }
    if (element.className) {
      script.className = element.className;
    }
    if (element.type) {
      script.type = element.type;
    }
    if (element.src) {
      script.src = element.src;
      // Force synchronous loading of peripheral JS.
      script.async = false;
    }
    if (element.dataset.pjax !== undefined) {
      script.dataset.pjax = '';
    }
    if (code !== '') {
      script.appendChild(document.createTextNode(code));
    }
    parent.appendChild(script);
  });

  
  NexT.boot.refresh();
  
  // Define Motion Sequence & Bootstrap Motion.
  if (CONFIG.motion.enable) {
    NexT.motion.integrator
      .init()
      .add(NexT.motion.middleWares.subMenu)
      .add(NexT.motion.middleWares.postList)
      .bootstrap();
  }
  
  NexT.utils.updateSidebarPosition();
  
- $(document).ready(function () {
-     if(location.href.indexOf("#reloaded")==-1){
-         location.href=location.href+"#reloaded";
-         location.reload();
-     }
- }）
  
});
</script>
```



### 版本控制

强烈建议无论是否以VSCode为主力编辑器都下载一个，它的git版本控制插件让我可以进行一些测试并以GUI可视化的方式回滚。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511224836320.png)

