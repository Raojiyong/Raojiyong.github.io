---
title: Anaconda3安装Pytorch
author: Jiyong Rao
date: 2021-05-06 17:00:00 +0800
categories: ["2021", "05"]
tags: [tutorial]
---

### 引言

在Win10下，通过在Anaconda3安装Pytorch，版本号为1.8.1。需要使用NVIDIA显卡，安装CUDA 11.1 和cuDNN。具体包含Anaconda3下载安装，同时给了常见出错问题急解决方法。

### Anaconda3安装

我是在 [anaconda3](https://docs.anaconda.com/anaconda/install/windows/) 官方网站上下载的，然后从上往下下载最新的版本。

下载好之后要注意安装问题，首先所针对用户，我选择的是针对该电脑的全部用户

 - [ ] Just Me
 - [x] For all users

之后是环境变量勾选，我没有勾选，系统推荐也是不勾选，之后再系统环境变量中添加就行，官方给的理由是会干扰到其他软件，没添加的话就没办法在cmd中运行。

安装完成之后可以在[这个博客](https://www.cnblogs.com/dereen/p/anaconda_tencent_mirrors.html)完成镜像源的切换，在`C:\Users\User_name\.condarc`文件中更改，例如，清华源可以

```
channels:
  - defaults
show_channel_urls: true
channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

我用清华源的时候出现各种问题，头大，删了anaconda重装后没配置`.condarc`文件，才顺利，源问题还是看其它blog吧。

### 创建conda环境

在对应anaconda目录下启动终端

`conda create -n py38 python=3.8`

然后`conda activate py38`进入环境。。

[CUDA下载链接](https://developer.nvidia.com/cuda-downloads)，[cuDNN下载链接](https://developer.nvidia.com/feedback/ws-gpu-2021-04)

将cuDNN下载后的压缩包解压，将bin、include、lib文件夹复制到CUDA对应目录。不会产生覆盖，因为是新文件。

### 安装pytorch

安装完CUDA和cuDNN后再切入py38环境，输入

`conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch -c nvidia -c conda-forge`

因为是11.1版本的CUDA，官方文档上说要加上conda-forge。

如果网速不稳定，或者镜像源不稳定，安装时可能会出现`CondaHTTPError`，重新下载几次也不行，就用迅雷下载，再进行安装。根据镜像源提供的网址，将未下载成功的文件离线下载，之后移动到Anaconda3安装目录的pkgs文件夹里，替换文件。然后打开pkgs文件里一个url命名的txt文本文件，将之前复制的下载链接复制到该txt中。

**virtualenv虚拟环境，创建不同版本的python虚拟环境**

