---
title: ios抓包tip
date: 2022-09-16 16:19:51
categories: [信息安全	,抓包]
swiper: true # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/002L7iXJgy1guzjnj7n6tj64mo2lrx6u02.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/002L7iXJgy1guzjnj7n6tj64mo2lrx6u02.jpg' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---
app不走系统代理？如何抓包？

> 之前遇到了一个问题iphone上的应用抓不到数据包。就是抓不到。
> 最初以为是像微信一样走了其他的协议。觉得这种应用他们也没有必要下这样的功夫这样的成本，肯定还是走的http
> 于是有了这个经历

# 简而言之，他们不走系统代理


网络请求代理设置NO_PROXY
- android系统设置的代理并不是强制对所有app生效的
- app可以在网络请求类库中通过自定义代理设置，选择是否要走系统代理
## 安卓怎么办呢

在网上找到了很多安卓的方法
不要用手机wifi的地方设置系统代理，那是系统代理不是全局代理
既然不走系统代理，那么直接抓系统的包不就可以了吗

被抓包的APP并不知道自己被套在了第几层

 - 方案一

使用proxifier 将模拟器请求直接转发到抓包软件，相当于抓安卓系统的包

- 方案二

同理，使用本地VPN抓包软件，如抓包精灵

- 方案三

justtrustme或者直接okhttp代理方法，使代理设置语句无效

直接放弃。首先安卓root装证书越来越麻烦，烦，证书都装不上看什么https。其次，我的安卓机没有电呀。用ios挺好。

## iOS怎么办呢
shadowrocket设置全局代理，好的解决。有个配置要叮嘱一下
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/IMG_81AA94E2F3D4-1.jpeg)
类型选择http。
## 总结
如果这也算提高攻击门槛的话，好吧可能确实有一点点点用处吧