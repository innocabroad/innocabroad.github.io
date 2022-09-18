---
title: matlab操作手册
date: 2022-09-16 13:40:42
tags: [数据建模,matlab,操作手册]
categories: [数据建模,matlab,操作手册]
swiper: true # 将文章放入轮播图中
swiperImg: '' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: '' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: 
---
- Matlab中的读取使用操作
```matlab
load('/Users/innocence/Downloads/data.mat');
```

-  errorbar - 含误差条的线图
    此 MATLAB 函数 创建 y 中数据的线图，并在每个数据点处绘制一个垂直误差条。err 中的值确
    定数据点上方和下方的每个误差条的长度，因此，总误差条长度是 err 值的两倍。
-  line - 创建基本线条
    此 MATLAB 函数 使用向量 x 和 y 中的数据在当前坐标区中绘制线条。如果 x 和 y 中有一个
    是矩阵或两者都是矩阵，则 line 将绘制多个线条。与 plot 函数不同，line 会向当前坐标区
    添加线条，而不删除其他图形对象或重置坐标区属性。