---
title: Mac环境安装imagemagick及使用imagemagick拼接图片
date: 2022-09-18 15:26:28
tags: [imagemagick,mac软件,图片处理]
categories: [imagemagick,mac软件,图片处理]
swiper: false # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8601a18b87d6277f8394ed1327381f30e924fc13-c5e07d98.png' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8601a18b87d6277f8394ed1327381f30e924fc13-c5e07d98.png' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---
## 安装
```
brew install ImageMagick
```
1. 安装：ImageMagick：

命令：brew install ImageMagick

这种方式安装下来的imageMagic，不缺少东西，报错较少。安装之后的位置处于：

/usr/local/Cellar/imagemagick/

2. 安装php扩展imagick

下载：wget https://pecl.php.net/get/imagick-3.4.3.tgz

解压：sudo tar -zxvf imagick-3.4.3

安装：

cd imagick-3.4.3

sudo /usr/bin/phpize

export PKG_CONFIG_PATH=/usr/local/Cellar/imagemagick/7.0.8-12_1/lib/pkgconfig


