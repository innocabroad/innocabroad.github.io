---
layout: latex
title: texlive更新安装宏包
date: 2022-09-18 13:04:58
tags: [latex]
categories: [latex]
swiper: false # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-18 13.09.52.png' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-18 13.09.52.png' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---

## 修改 Tex Live 镜像源

>【参考】https://developer.aliyun.com/mirror/CTAN
>此处使用阿里云镜像站 CTAN 镜像源临时切换，可以用如下命令：

# update --all 参数可根据需要修改
```
tlmgr update --all --repository https://mirrors.aliyun.com/CTAN/systems/texlive/tlnet
```
长期更换，可以使用如下命令：
```
tlmgr option repository https://mirrors.aliyun.com/CTAN/systems/texlive/tlnet
```
安装宏包
```
tlmgr install <packagename>
```
移除
```
tlmgr remove <packagename>
```
查看所有更新的宏包指令：
```
tlmgr update --list
```
更新所有需要更新的宏包
```
tlmgr update --self --all

```
如果遇到更新宏包过程中，某一个宏包更新失败，可以使用指令继续更新：
```
tlmgr update --reinstall-forcibly-removed --all
```
这里的tlmgr就相当于Python中的pip，tlmgr是 Tex Live Package Manger

进阶选手可以选择上述更新清单中自己想更新的宏包进行更新。
```
tlmgr update --usepackage_name
```