---
title: hexo搭建博客踩坑记录
<!-- date: 2020-03-18 22:05:31 -->
categories: hexo
---
### npm node的版本
无论是`npm`还是`node.js`的版本都要高一些，不然会有很多包安装不上，出现n多问题。我的博客node.js为v12.16.1，npm版本为6.14.2。

### root地址要修改
由于觉得github项目名取为`***.github.io`太长，所以直接取名为blog，最终博客地址为https://janicewuo.github.io/blog/ <br/>
<!--more-->
这样在本地项目根目录的_config.yml中要将root改为/blog/而不是像其他有些教程那样写成/blog。这里的root不改对会直接导致页面加载不出css、jquery等样式文件。

### 关于hexo d
每次执行`hexo d`之后，其实要差不多半分钟页面才会更新，所以手动刷新一两次页面没变可能并不是代码问题。建议先执行`hexo s`生成静态页面，进入[localhost:4000](http://localhost:4000)查看。

### 关于创建新文章
刚刚通过hexo new post创建了一个名为article2的文章，deploy g成功，deploy s成功，但是刷新网页并没有文章更新。接着尝试deploy d也部署成功，可就是没有显示新文章。<br/>
经过排查，是自己输入的命令有误：
```bash
hexo new post "article2"
```
虽然这样在_posts下也会生成正确的`article2.md`文件，但最终hexo并不能正确捕捉到这个文件并传入服务器。正确命令应该为：
```bash
hexo new post article
```
不能加引号，切记。