---
title: hexo+github+PicGo搭建图床
date: 2022-09-15 16:18:08
tags: [hexo,图床]
categories: 功能教程
swiper: true # 将文章放入轮播图中
swiperImg: '/medias/1.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/004fvDbLly1gubxqskjqsj635s23ub2k02.jpg' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---
{% title h1, hexo+github+PicGo搭建图床 %}


{% title h2, 搭建github仓库图床%}


1.登录/注册GitHub，新建一个仓库，填写好仓库名，仓库描述，根据需求选择是否为仓库初始化一个README.md描述文件

2.在主页依次选择【Settings】-【Developer settings】-【Personal access tokens】-【Generate new token】，填写好描述，勾选【repo】，然后点击【Generate token】生成一个Token，注意这个Token只会显示一次，自己先保存下来，或者等后面配置好PicGo后再关闭此网页


{% title h2, 配置PicGo%}

前往下载[PicGo](https://github.com/Molunerfinn/PicGo/releases)，安装好后开始配置图床

设定仓库名：按照【用户名/图床仓库名】的格式填写

设定分支名：【main】

设定Token：粘贴之前生成的【Token】

指定存储路径：填写想要储存的路径，如【img/】，这样就会在仓库下创建一个名为 img 的文件夹，图片将会储存在此文件夹中


{% title h2, 设定自定义域名%}

它的作用是，在图片上传后，PicGo 会按照【自定义域名+储存路径+上传的图片名】的方式生成访问链接，并放到粘贴板上，因为我们要使用 jsDelivr 加速访问，所以可以设置为【https://cdn.jsdelivr.net/gh/用户名/图床仓库名 】，上传完毕后，我们就可以通过【https://cdn.jsdelivr.net/gh/用户名/图床仓库名/图片路径 】加速访问我们的图片了，比如上图的图片链接为：https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/004fvDbLly1gubxqskjqsj635s23ub2k02.jpg
至此免费图床搭建完成。可以使用PicGo 工具 愉快的上传图片了，直接粘贴在markdown博客编写工具中就可以了。
图片不能重复上传，因为都会在同一个目录下，重复上传会有重名错误。

{% title h2, 进行图片上传%}

配置好PicGo后，我们就可以进行高效创作了，将图片拖拽到上传区，将会自动上传并复制访问链接，将链接粘贴到博文中就行了，访问速度杠杠的，此外PicGo还有相册功能，可以对已上传的图片进行删除，修改链接等快捷操作，PicGo还可以生成不同格式的链接、支持批量上传、快捷键上传、自定义链接格式、上传前重命名等，更多功能自己去探索吧！
