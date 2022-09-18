---
title: python与神经网络
date: 2022-09-17 15:17:07
tags: [数据建模,神经网络,python]
categories: [数据建模方法,神经网络,python]
swiper: true # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8601a18b87d6277f8394ed1327381f30e924fc13-c5e07d98.png' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8601a18b87d6277f8394ed1327381f30e924fc13-c5e07d98.png' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---
# python pip库 sklearn、torch、tensorflow
 
torch [官方文档](https://pytorch.org/docs/stable/torch.html) [中文文档](https://pytorch.apachecn.org/#/)
python torch又称PyTorach，是一个以Python优先的深度学习框架，一个开源的Python机器学习库，用于自然语言处理等应用程序，不仅能够实现强大的GPU加速，同时还支持动态神经网络，这是现在很多主流框架比如Tensorflow等都不支持的。

>pip3 install torchvision
>pip3 install torch

sklearn [中文文档](https://www.sklearncn.cn)
scikit-learn是基于Python语言的机器学习库，具有：
- 简单高效的数据分析工具
- 可在多种环境中重复使用
- 建立在Numpy，Scipy以及matplotlib等数据科学库之上
- 开源且可商用的-基于BSD许可

tensorflow [官方文档](https://www.tensorflow.org) [中文文档](https://www.w3cschool.cn/tensorflow_python/.html)
TensorFlow由谷歌人工智能团队谷歌大脑（Google Brain）开发和维护，拥有包括TensorFlow Hub、TensorFlow Lite、TensorFlow Research Cloud在内的多个项目以及各类应用程序接口（Application Programming Interface, API） [2]  。自2015年11月9日起，TensorFlow依据阿帕奇授权协议（Apache 2.0 open source license）开放源代码 [2]  。
# torch
## [张量](https://blog.csdn.net/z240626191s/article/details/124204965)
写个demo就遇到了各种各样的bug
1. 下载Pytorch的自带数据集时报错=urllib.error.URLError: urlopen error [SSL: CERTIFICATE_VERIFY_FAILED]
### 错误原因：
这是一个SSL证书验证错误，当请求一个https站点，但是证书验证错误时，就会报这样的错误。
### 解决办法：
只需在代码中加入如下两行将跳过证书的检查，即可成功访问网页。
```
# 全局取消证书验证
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
```
2. 【PyTorch教程】04-详解torchvision 0.13中的预训练模型加载的更新及报错的解决方法 (2022年最新)
加载预训练模型(有重大更新)

相信最近 (2022年7月) 安装或者更新了 PyTorch 和 torchvision 的同志们可能跑代码时遇到了下面的报错之一：
```
UserWarning: The parameter ‘pretrained’ is deprecated since 0.13 and will be removed in 0.15, please use ‘weights’ instead.

UserWarning: Arguments other than a weight enum or None for ‘weights’ are deprecated since 0.13 and will be removed in 0.15. The current behavior is equivalent to passing weights=ResNet50_Weights.IMAGENET1K_V1. You can also use weights=ResNet50_Weights.DEFAULT to get the most up-to-date weights.

Expected type ‘Optional[ResNet50_Weights]’, got ‘str’ instead
```
这是因为 torchvision 0.13对预训练模型加载方式作出了重大更新造成的。今天一次性就可以把上面3条Bug全部消灭。

1. 新老版本写法对比

>从 torchvision 0.13开始，加载预训练模型函数的参数从 pretrained = True 改为 weights=预训练模型参数版本 。且旧版本的写法将在未来的torchvision 0.15版本中被Deprecated 。

举个例子：

```python
from torchvision import models

# 旧版本的写法，将在未来的torchvision 0.15版本中被Deprecated
model_old = models.resnet50(pretrained=True) # deprecated
model_old = models.resnet50(True) # deprecated

# torchvision 0.13及以后的新版本写法
model_new = models.resnet50(weights=models.ResNet50_Weights.IMAGENET1K_V1)
# 没有预训练模型加载
model = models.resnet50(weights=None)
model = models.resnet50()

```
其中，第8行代码的 IMAGENET1K_V1 表示的是 ResNet-50 在 ImageNet 数据集上进行预训练的第一个版本的权重参数文件。是一个版本标识符。

2. 新写法的好处

在旧版本的写法 pretrained = True 中，对于预训练权重参数我们没有太多选择的余地，一执行起来就要使用默认的预训练权重文件版本。但问题是，现在深度学习的发展日新月异，很快就有性能更强的模型横空出世。

而使用新版本写法 weights=预训练模型参数版本 ，相当于我们掌握了预训练权重参数文件的选择权。我们就可以尽情地使用更准更快更强更新的预训练权重参数文件，帮助我们的研究更上一层楼。

举个例子：

```python
from torchvision import models

# 加载精度为76.130%的旧权重参数文件V1
model_v1 = models.resnet50(weights=models.ResNet50_Weights.IMAGENET1K_V1)
# 等价写法
model_v1 = models.resnet50(weights="IMAGENET1K_V1")

# 加载精度为80.858%的新权重参数文件V2
model_v2 = models.resnet50(weights=models.ResNet50_Weights.IMAGENET1K_V2)
# 等价写法
model_v1 = models.resnet50(weights="IMAGENET1K_V2")

```
如果你不知道哪个权重文件的版本是最新的，没关系，直接选择默认DEFAULT即可。官方会随着 torchvision 的升级而让 DEFAULT 权重文件版本保持在最新。如下代码所示：
```python
from torchvision import models

# 如果你不知道哪个版本是最新, 直接选择默认DEFAULT即可
model_new = models.resnet50(weights=models.ResNet50_Weights.DEFAULT)

```

在中文模版中没有更新
代码应该进行修改
> 从torchvision加载了经过预训练的 resnet18 模型。 我们创建一个随机数据张量来表示具有 3 个通道的单个图像，高度&宽度为 64，其对应的label初始化为一些随机值。
## [resnet18模型](https://blog.csdn.net/Chenzhinan1219/article/details/122042407)
```python
import torch
from torchvision.models import resnet18, ResNet18_Weights
model = resnet18(weights=ResNet18_Weights.DEFAULT)
data = torch.rand(1, 3, 64, 64)
labels = torch.rand(1, 1000)
prediction = model(data) # forward pass
loss = (prediction - labels).sum()#用模型的预测和相应的标签来计算误差
loss.backward() #  当我们在误差张量上调用.backward()时，开始反向传播. 然后，Autograd 会为每个模型参数计算梯度并将其存储在参数的.grad属性中。
optim = torch.optim.SGD(model.parameters(), lr=1e-2, momentum=0.9)#接下来，我们加载一个优化器，在这种情况下，SGD的学习率为0.01，动量为0.9。我们在优化器中注册模型的所有参数。
optim.step() #最后，我们调用.step()启动梯度下降。 优化器通过.grad中存储的梯度来调整每个参数。
print(optim)

```

## Autograd 的微分


