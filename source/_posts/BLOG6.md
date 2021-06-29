---
title: 自动备份Hexo博客源文件
comment: false
tags:
  - Hexo
  - NexT
  - Blog
categories: 博客搭建 (Blog Building)
abbrlink: c4d910e6
date: 2021-06-29 13:36:41
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---











### 引言

Hexo+NexT一般是在本地部署的，最近需要换设备重新搭建博客，而`git`命令备份博客又比较繁琐，所以找到一篇关于自动备份源文件的博文：[自动备份Hexo博客源文件](https://wugenqiang.github.io/articles/auto_backup_blog_source_files.html)转载过来并稍做修改。



<!--more-->



### 原理

通过监听Hexo的事件来完成自动执行Git命令进行自动备份，查阅[Hexo文档](https://hexo.io/zh-cn/api/events.html)，找到了Hexo的主要事件，见下表：

|      事件名      |     事件发生时间     |
| :--------------: | :------------------: |
|  `deployBefore`  |   在部署完成前发布   |
|  `deployAfter`   |   在部署成功后发布   |
|      `exit`      |  在 Hexo 结束前发布  |
| `generateBefore` | 在静态文件生成前发布 |
| `generateAfter`  | 在静态文件生成后发布 |
|      `new`       | 在文章文件建立后发布 |



于是我们就可以通过监听Hexo的`deployAfter`事件，待上传完成之后自动运行Git备份命令，从而达到自动备份的目的。



### 实现

#### git上传仓库

本脚本需要提前将Hexo加入Git仓库并与Github或者Gitee远程仓库绑定之后，才能正常工作。如果你不知道该怎样进行操作，可以参考原博主的另一篇博文：

- [Git命令手动备份Hexo博客源文件](https://wugenqiang.gitee.io/articles/manual_backup_blog_source_files.html)



#### 安装`shelljs`模块

要实现这个自动备份功能，需要依赖NodeJs的一个shelljs模块,该模块重新包装了child_process,调用系统命令更加的方便。

```shell
npm install --save shelljs
```





#### 自动备份脚本

`shelljs`模块安装完成后，在`Hexo`根目录的`scripts`文件夹下新建一个js文件，文件名随意取(我的文件名为:`auto_backup.js`)。如果没有`scripts`目录，请新建一个。

然后在脚本中，写入以下内容：

```shell
require('shelljs/global');
try {
    hexo.on('deployAfter', function() {//当deploy完成后执行备份
        run();
    });

} catch (e) {
    console.log("产生了一个错误啊<(￣3￣)> !，错误详情为：" + e.toString());
}
function run() {
    if (!which('git')) {
        echo('Sorry, this script requires git');
        exit(1);
    } else {
        echo("======================Auto Backup Begin===========================");
        cd('/Users/apple/Desktop/blog');    //此处修改为Hexo根目录路径
        if (exec('git add --all').code !== 0) {
            echo('Error: Git add failed');
            exit(1);
        }
        if (exec('git commit -am "blog auto backup script\'s commit"').code !== 0) {
            echo('Error: Git commit failed');
            exit(1);
        }
        if (exec('git push origin main').code !== 0) {
            echo('Error: Git push failed');
            exit(1);
        }
        echo("==================Auto Backup Complete============================")
    }
}
```

- 其中，需要修改第16行的`/Users/apple/Desktop/blog`路径为Hexo的根目录路径。（脚本中的路径为博主的Hexo路径）
- 如果你的Git远程仓库名称不为`origin`的话，还需要修改第25行执行的`push`命令，修改成自己的远程仓库名和相应的分支名

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629135038618.png)





### 测试

`hexo -d`后成功上传。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629140447332.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629140808496.png)





### 参考文献

+ [自动备份Hexo博客源文件](https://wugenqiang.github.io/articles/auto_backup_blog_source_files.html)

