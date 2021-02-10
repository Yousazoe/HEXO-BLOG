---
title: Hero-NexT主题配置
tags:
  - Hexo
  - NexT
  - Blog
categories: 
  - 博客搭建 (Blog Building)
abbrlink: 3bcb4b40
date: 2021-01-26 16:55:34
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/008eGmZEly1gn4n8vkpmgj30ma09u40a.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="http://theme-next.iissnan.com/">Hexo NexT</a>
    </i>
  </font>
</div>



### 引言

本文记录NexT博客的主题配置，本文记录了从站点配置Hexo重新安装到NexT主题自带的基础配置，不包含带有插件安装的主题美化。

<!--more-->



### Hexo安装

```bash
npm install hexo-cli -g
```





### 获取NexT

#### 克隆最新版本

在终端窗口下，定位到 Hexo 站点目录下。使用 `Git` checkout 代码：

```shell
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```



#### 下载稳定版本

1. 前往 NexT 版本 [发布页面](https://github.com/iissnan/hexo-theme-next/releases)。
2. 选择你所需要的版本，下载 Download 区域下的 Source Code (zip) 到本地。例如，下载 v0.4.0 版本：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/008eGmZEly1gn173rzm2oj30o30art9c.jpg)

3. 解压所下载的压缩包至站点的 themes 目录下， 并将 解压后的文件夹名称（`hexo-theme-next-0.4.0`）更改为 `next`。





### 站点配置

与所有 Hexo 主题启用的模式一样。 当 克隆/下载 完成后，打开 **站点配置文件**， 找到 `theme` 字段，并将其值更改为 `next`。

启用 NexT 主题

```yaml
theme: next
```

到此，NexT 主题安装完成。下一步我们将验证主题是否正确启用。在切换主题之后、验证之前， 我们最好使用 `hexo clean` 来清除 Hexo 的缓存。

#### 验证主题

首先启动 Hexo 本地站点，并开启调试模式（即加上 `--debug`），整个命令是 `hexo s --debug`。 在服务启动的过程，注意观察命令行输出是否有任何异常信息，如果你碰到问题，这些信息将帮助他人更好的定位错误。 当命令行输出中提示出：

```bash
INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
```

此时即可使用浏览器访问 `http://localhost:4000`，检查站点是否正确运行。



#### 设置语言

编辑 **站点配置文件**， 将 `language` 设置成你所需要的语言。建议明确设置你所需要的语言，例如选用简体中文，配置如下：

```yaml
language: zh-Hans
```

目前 NexT 支持的语言如以下表格所示：

| 语言         | 代码                 | 设定示例                            |
| :----------- | :------------------- | :---------------------------------- |
| English      | `en`                 | `language: en`                      |
| 简体中文     | `zh-Hans`            | `language: zh-Hans`                 |
| Français     | `fr-FR`              | `language: fr-FR`                   |
| Português    | `pt`                 | `language: pt` or `language: pt-BR` |
| 繁體中文     | `zh-hk` 或者 `zh-tw` | `language: zh-hk`                   |
| Русский язык | `ru`                 | `language: ru`                      |
| Deutsch      | `de`                 | `language: de`                      |
| 日本語       | `ja`                 | `language: ja`                      |
| Indonesian   | `id`                 | `language: id`                      |
| Korean       | `ko`                 | `language: ko`                      |



### 主题配置

#### 选择主题

Scheme 是 NexT 提供的一种特性，借助于 Scheme，NexT 为你提供多种不同的外观。同时，几乎所有的配置都可以 在 Scheme 之间共用。目前 NexT 支持三种 Scheme，他们是：

- Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
- Mist - Muse 的紧凑版本，整洁有序的单栏外观
- Pisces - 双栏 Scheme，小家碧玉似的清新

Scheme 的切换通过更改 **主题配置文件**，搜索 scheme 关键字。 你会看到有三行 scheme 的配置，将你需用启用的 scheme 前面注释 `#` 去除即可。

```yaml
# Schemes
- scheme: Muse
+ #scheme: Muse
#scheme: Mist
#scheme: Pisces
- #scheme: Gemini
+ scheme: Gemini
```





#### 设置侧栏

默认情况下，侧栏仅在文章页面（拥有目录列表）时才显示，并放置于右侧位置。 可以通过修改 **主题配置文件** 中的 `sidebar` 字段来控制侧栏的行为。侧栏的设置包括两个部分，其一是侧栏的位置， 其二是侧栏显示的时机。

1. 设置侧栏的位置，修改 `sidebar.position` 的值，支持的选项有：

   - left - 靠左放置
   - right - 靠右放置

   目前仅 Pisces Scheme 支持 `position` 配置。影响版本**5.0.0**及更低版本。

   ```yaml
   sidebar:
     position: left
   ```

2. 设置侧栏显示的时机，修改 `sidebar.display` 的值，支持的选项有：

   - `post` - 默认行为，在文章页面（拥有目录列表）时显示
   - `always` - 在所有页面中都显示
   - `hide` - 在所有页面中都隐藏（可以手动展开）
   - `remove` - 完全移除

   ```yaml
   sidebar:
     display: post
   ```





#### 添加「标签」页面

新建「标签」页面，并在菜单中显示「标签」链接。「标签」页面将展示站点的所有标签，若你的所有文章都未包含标签，此页面将是空的。 

##### 新建页面

在终端窗口下，定位到 Hexo 站点目录下。使用 `hexo new page` 新建一个页面，命名为 `tags` ：

```shell
$ cd your-hexo-site
$ hexo new page tags
```

##### 设置页面类型

编辑刚新建的页面，将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：

```markdown
---
title: 标签
date: 2014-12-22 12:39:04
type: "tags"
---
```



#### 添加「分类」页面

新建「分类」页面，并在菜单中显示「分类」链接。「分类」页面将展示站点的所有分类，若你的所有文章都未包含分类，此页面将是空的。

##### 新建页面

在终端窗口下，定位到 Hexo 站点目录下。使用 `hexo new page` 新建一个页面，命名为 `categories` ：

```shell
$ cd your-hexo-site
$ hexo new page categories
```

##### 设置页面类型

编辑刚新建的页面，将页面的 `type` 设置为 `categories` ，主题将自动为这个页面显示分类。页面内容如下：

```markdown
---
title: 分类
date: 2014-12-22 12:39:04
type: "categories"
---
```





#### 更改头像

编辑主题配置文件，修改 `avatar`， 值设置成头像的链接地址。其中，头像的链接地址可以是：

地址值完整的互联网 URL`http://example.com/avatar.png`站点内的地址将头像放置主题目录下的 `source/uploads/` （新建 uploads 目录若不存在） 配置为：`avatar: /uploads/avatar.png` 或者放置在 `source/images/` 目录下配置为：`avatar: /images/avatar.png`：

```yaml
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: /images/cat.png
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```





#### 更改网站图标

将默认的图片路径换为自己的路径或者链接：

```yaml
favicon:
-  small: /images/favicon-16x16-next.png
-  medium: /images/favicon-32x32-next.png
-  apple_touch_icon: /images/apple-touch-icon-next.png
-  safari_pinned_tab: /images/logo.svg
+  small: /images/favicon.ico
+  medium: /images/favicon.ico
+  apple_touch_icon: /images/favicon.ico
+  safari_pinned_tab: /images/favicon.ico
	#android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```





#### 侧边栏社交信息

编辑主题配置文件`_config.yml`，修改`social`字段的值：

```yaml
# Social Links
# Usage: `Key: permalink || icon`
# Key is the link label showing to end users.
# Value before `||` delimiter is the target permalink, value after `||` delimiter is the name of Font Awesome icon.
social:
  GitHub: https://github.com/Yousazoe || fab fa-github
  #E-Mail: mailto:yourname@gmail.com || fa fa-envelope
  #Weibo: https://weibo.com/yourname || fab fa-weibo
  #Google: https://plus.google.com/yourname || fab fa-google
  #Twitter: https://twitter.com/yourname || fab fa-twitter
  #FB Page: https://www.facebook.com/yourname || fab fa-facebook
  #StackOverflow: https://stackoverflow.com/yourname || fab fa-stack-overflow
  #YouTube: https://youtube.com/yourname || fab fa-youtube
  #Instagram: https://instagram.com/yourname || fab fa-instagram
  #Skype: skype:yourname?call|chat || fab fa-skype

social_icons:
  enable: true
  icons_only: ture
  transition: false
```





#### 代码高亮主题

NexT 使用 [Tomorrow Theme](https://github.com/chriskempson/tomorrow-theme) 作为代码高亮，共有5款主题供你选择。 NexT 默认使用的是 白色的 `normal` 主题，可选的值有 `normal`，`night`， `night blue`， `night bright`， `night eighties`：

| ![](https://tva1.sinaimg.cn/large/008eGmZEly1gn3h06njcoj309d0ck74q.jpg) | ![](https://tva1.sinaimg.cn/large/008eGmZEly1gn3h07gs37j309d0ckmxm.jpg) | ![](https://tva1.sinaimg.cn/large/008eGmZEly1gn3h08bjtbj309d0ckaaj.jpg) | ![](https://tva1.sinaimg.cn/large/008eGmZEly1gn3h098mnij309d0ckaai.jpg) | ![](https://tva1.sinaimg.cn/large/008eGmZEly1gn3h0ac07kj309d0ckgm2.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |                                                              |                                                              |                                                              |

更改 `highlight_theme` 字段，将其值设定成你所喜爱的高亮主题，例如：

高亮主题设置示例

```yaml
# Code Highlight theme
# Available value: normal | night | night eighties | night blue | night bright
# https://github.com/chriskempson/tomorrow-theme
highlight_theme: normal
```



#### 阅读进度条

我们可以在主题配置文件`_config.yml` 中进行修改：

```yaml
# Reading progress bar
reading_progress:
  enable: ture
  # Available values: top | bottom
  position: top
  color: "#37c6c0"
  height: 3px
```

注意：**这个阅读进度条动画需要安装依赖**，地址：[Reading Progress for NexT](https://github.com/theme-next/theme-next-reading-progress)。

- 方法 1：安装文件

```bash
# 进入主题目录
cd themes/next

# 从GitHub下载依赖文件
git clone https://github.com/theme-next/theme-next-reading-progress source/lib/reading_progress
```

- 方法 2：启用 CDN

我们可以在主题配置文件`_config.yml` 中修改：

```yaml
vendors:
  reading_progress: //cdn.jsdelivr.net/gh/theme-next/theme-next-reading-progress@1/reading_progress.min.js
```



#### 阅读百分比&底部返回

在主题配置文件`_config.yml` 中修改：

```yaml
back2top:
  enable: ture
  # Back to top in sidebar.
  sidebar: false
  # Scroll percent label in b2t button.
  scrollpercent: ture
```





#### 动态彩带背景

我们可以在主题配置文件`_config.yml` 中修改：

```yaml
# JavaScript 3D library.
# Dependencies: https://github.com/theme-next/theme-next-three
three:
  enable: ture
  three_waves: false
  canvas_lines: ture
  canvas_sphere: false
```

接着替换原先的CDN：

```yaml
	# Internal version: 1.0.0
  # three: //cdn.jsdelivr.net/gh/theme-next/theme-next-three@1/three.min.js
  # three_waves: //cdn.jsdelivr.net/gh/theme-next/theme-next-three@1/three-waves.min.js
  # canvas_lines: //cdn.jsdelivr.net/gh/theme-next/theme-next-three@1/canvas_lines.min.js
  # canvas_sphere: //cdn.jsdelivr.net/gh/theme-next/theme-next-three@1/canvas_sphere.min.js
  three:
  three_waves:
  canvas_lines: //cdn.jsdelivr.net/gh/bynotes/texiao/source/js/caidai.js # 动态彩带
  canvas_sphere:
```



#### 边框圆角

在`themes/next-reloaded/source/css/_variables/Gemini.styl`中添加如下代码：

```stylus
// 修改主题页面布局为圆角
$border-radius-inner = 15px 15px 15px 15px;
$border-radius = 15px;
```



#### 公益404页面

腾讯公益404页面，寻找丢失儿童，让大家一起关注此项公益事业！效果如下 http://www.ixirong.com/404.html

使用方法，新建 404.html 页面，放到主题的 `source` 目录下，内容如下：

```html
<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="robots" content="all" />
  <meta name="robots" content="index,follow"/>
  <link rel="stylesheet" type="text/css" href="https://qzone.qq.com/gy/404/style/404style.css">
</head>
<body>
  <script type="text/plain" src="http://www.qq.com/404/search_children.js"
          charset="utf-8" homePageUrl="/"
          homePageName="回到我的主页">
  </script>
  <script src="https://qzone.qq.com/gy/404/data.js" charset="utf-8"></script>
  <script src="https://qzone.qq.com/gy/404/page.js" charset="utf-8"></script>
</body>
</html>
```



#### 简繁体切换

简体繁体切换的基本原理：首先建立一个简体字与繁体字相对应的映射表，然后遍历整个界面，把相应的简体字或者是繁体字映射为对应的字体即可。



##### Hexo 实现过程

1. 首先，我们可以在[这里](https://tding.top/js/tw_cn.js)右键另存下载简繁字体切换所需的 `tw_cn.js` 文件，我们把这个文件放到 `~/themes/next/source/js` 文件夹下。
2. **修改模板**，在我们想要显示简繁转换按钮的地方添加如下代码。例如，我在 NexT 主题的布局文件 `~/themes/next/layout/_partials/footer.swig` 里添加了如下代码：

```html
<div class="translate-style">
繁/简：<a id="translateLink" href="javascript:translatePage();">繁体
</a>
</div>
<script type="text/javascript" src="/js/tw_cn.js"></script>
<script type="text/javascript">
var defaultEncoding = 2; //网站编写字体是否繁体，1-繁体，2-简体
var translateDelay = 0; //延迟时间,若不在前, 要设定延迟翻译时间, 如100表示100ms,默认为0
var cookieDomain = "https://tding.top/"; //Cookie地址, 一定要设定, 通常为你的网址
var msgToTraditionalChinese = "繁体"; //此处可以更改为你想要显示的文字
var msgToSimplifiedChinese = "简体"; //同上，但两处均不建议更改
var translateButtonId = "translateLink"; //默认互换id
translateInitilization();
</script>
```

读者可以在**博客底部点击简体 / 繁体**来看具体的切换字体效果。

##### 参考

- [三步让你的网站支持简体繁体切换](https://www.arao.me/website/hexo-support-jian-fan-language.html#more)
- [两步让你的网站支持简体繁体切换](http://qingbo.site/2016/10/11/how-set-Chinese-Simplified-switch-to-Chinese-Traditional/)



