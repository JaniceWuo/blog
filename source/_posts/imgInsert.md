---
title: hexo文章插入本地图片失败
date: 2020-03-22 22:30:37
categories:
- hexo
---
之前插入本地图片一直失败，已经按照教程修改了`_config.yml`下的`post_asset_folder: true`，而且也安装了hexo-asset-image，把图片image.jpg放进文章同名的文件夹322内，markdown写入`![](322/image.jpg)`，执行hexo s图片显示失败。<br/>
好，开始找原因。<br/>
按F12查找源码，发现图片路径为`http://localhost:4000/2020/03/22/322/image.jpg`，链接复制粘贴到浏览器确实没有图片，但是在本地public/2020/03/22/322下已经生成了image.jpg。这就很无语了...<br/>
然后我仔细查看了路径，试着改为`http://localhost:4000/blog/2020/03/22/322/image.jpg`，发现成功显示图片！（我的博客本地打开后是`localhost:4000/blog/`）。于是在hexo根目录下的_config.yml末尾添加:
<!--more-->
```
imgroot: /blog/
```
其中`blog`改为你自己的博客名，然后执行
```
hexo clean
hexo g
hexo s
```
即可成功在文章中插入图片。