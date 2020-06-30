---
title: NVIDIA-SMI has failed because it couldn’t communicate with the NVIDIA driver解决方案
date: 2020-03-20 17:45:27
categories: nvidia
---
在租用某大厂服务器时，输入`nvcc -V`显示nvcc没有安装，但是服务器确实是装了cuda和cudnn的，于是输入`vim ~/.bashrc`在行末尾加上：
```bash
export PATH=$PATH:/usr/local/cuda/bin
export LD_LIBRARY_PATH=/usr/local/cuda/lib64::$LD_LIBRARY_PATH
```
然后执行`source ~/.bashrc`，之后`nvcc -V`成功输出信息。<br/>
以为终于可以成功用上tensorflow-gpu版了，写了个简单的test.py测试一下，结果输出结果还是在cpu上跑的。我就很无语了，cuda啥的都装上了，tensorflow-gpu也装成功，为啥还是使用的cpu。接着输入`nvidia-smi`查看显卡，出现“NVIDIA-SMI has failed because it couldn’t communicate with the NVIDIA driver”......
谷歌之后发现解决方案：<br/>
<!--more-->
输入命令:
```bash
sudo apt-get install dkms
```
查看nvidia版本号
```bash
ls /usr/src/
```
发现服务器的nvidia版本号为440.36，于是输入命令：
```bash
sudo dkms build -m nvidia -v 440.36
sudo dkms install -m nvidia -v 440.36
```
输入`nvidia-smi`能显示显卡信息，此时也能成功使用gpu了。