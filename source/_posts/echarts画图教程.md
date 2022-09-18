---
title: echarts画图教程
date: 2022-09-16 19:19:27
tags: [echarts,数学建模]
categories: [echarts,数学建模]
swiper:  # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-16%2019.20.42.png' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-16%2019.20.42.png' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
---
spss pro 智能画图更方便
https://www.spsspro.com/prodraw/operation/2666341?name=红酒数据.xlsx
直接表格拖入数据即可
# 获取安装 echart & jquery
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/echarts.js)
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/jquery-1.9.1.min.js)
新建目录js存放js脚本
在项目目录新建一个index.html 文件，内容如下：
```html

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Echarts入门案例</title>
<!-- 引入 开发环境的echarts.js -->
<script src="js/echarts.js"></script>
<script src="js/jquery-1.9.1.min.js"></script>
<script src="js/index.js"></script>

<!-- 声明DOM容器对象,为ECharts准备一个具备大小（宽高）的Dom -->
<style type="text/css">
#main{
	width: 600px;
	height:400px;
}
</style>
</head>
<body>
	<div id="main">
	</div>

</body>
</html>

```
index.js中插入[示例](https://echarts.apache.org/examples/zh/index.html)开头结尾要包括
```
$(document).ready(function(){
	  });
```

画图参考https://echarts.apache.org/examples/zh/index.html#chart-type-line
挑选需要的图片读入数据



