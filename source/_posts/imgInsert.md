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
即可成功在文章中插入图片。<br/>
补充：关于`asset-image`插件，安装后需要修改package.json源码，如下：
```json
{
  "_from": "hexo-asset-image@^1.0.0",
  "_id": "hexo-asset-image@1.0.0",
  "_inBundle": false,
  "_integrity": "sha512-jkuUJNPRMH6v7HqzP2BAwEZavMzVxNWhl8jZl9BmFYB22/aq2+zixGIhV4vedI9cLPydjn9DfII41/MMXtzJTA==",
  "_location": "/hexo-asset-image",
  "_phantomChildren": {},
  "_requested": {
    "type": "range",
    "registry": true,
    "raw": "hexo-asset-image@^1.0.0",
    "name": "hexo-asset-image",
    "escapedName": "hexo-asset-image",
    "rawSpec": "^1.0.0",
    "saveSpec": null,
    "fetchSpec": "^1.0.0"
  },
  "_requiredBy": [
    "#USER",
    "/"
  ],
  "_resolved": "https://registry.npmjs.org/hexo-asset-image/-/hexo-asset-image-1.0.0.tgz",
  "_shasum": "f229ad28b071a32b1d5b121f929a296e714fd24a",
  "_spec": "hexo-asset-image@^1.0.0",
  "_where": "E:\\github\\blog",
  "author": {
    "name": "xcodebuild"
  },
  "bundleDependencies": false,
  "dependencies": {
    "cheerio": "^0.19.0",
    "entities": "^1.1.2"
  },
  "deprecated": false,
  "description": "Give asset image in hexo a absolutely path automatically",
  "keywords": [
    "hexo",
    "iamge",
    "asset",
    "path"
  ],
  "license": "MIT",
  "main": "index.js",
  "name": "hexo-asset-image",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "version": "1.0.0"
}

```
里面的_where修改为自己的项目路径。