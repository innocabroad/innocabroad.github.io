---
title: bp神经网络
date: 2022-09-17 14:14:35
tags: [数据建模方法,bp神经网络]
categories: [数据建模方法,bp神经网络]
swiper: true # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8601a18b87d6277f8394ed1327381f30e924fc13-c5e07d98.png' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8601a18b87d6277f8394ed1327381f30e924fc13-c5e07d98.png' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---
# bp神经网络分类

## 1、作用
单层神经元学习能力非常有限，故而添加多个神经元，将神经元分为多层，它们不存在跨层连接，也没有同层连接，每层神经元和下一级神经元完全互连，这样的神经网络被称为“多层前馈网络”。其中，输入层神经元只负责输入，隐层神经元和输出层神经元都包含功能神经元，即包含激活函数。学习的过程即根据训练数据来调节神经元之间的“连接权”，以及功能神经元的阈值。
M-P 神经元模型
模拟神经元，通过函数将输入的向量转化为输出。
![](https://b3logfile.com/file/2020/07/v27ccb6a3a5ec57607cf837fe0f9b98055720w-92c1c139.jpg?imageView2/2/interlace/1/format/jpg)

​bp神经网络是一种按误差逆传播算法训练的多层前馈网络，是目前应用最广泛的神经网络模型之一。bp神经网络的学习规则是使用最速下降法，通过反向传播来不断调整网络的权值和阈值，使网络的分类错误率最小。


## 2、输入输出描述
输入：自变量X为1个或1个以上的定类或定量变量，因变量Y为一个定类变量。
输出：模型的分类结果和模型分类的评价效果。
​
## 3、案例示例
根据红酒的颜色强度，脯氨酸，类黄酮等变量，生成一个能够区分琴酒，雪莉，贝尔摩德三种品种的红酒的bp神经网络。
导入数据

# 5、案例操作

Step1：新建分析；
Step2：上传数据；
Step3：选择对应数据打开后进行预览，确认无误后点击开始分析；
step4：选择【bp神经网络分类】；
step5：查看对应的数据数据格式，按要求输入【bp神经网络分类】数据;
step6：进行参数设置（“更多设置”里的参数在客户端可进行设定）
step7：点击【开始分析】，完成全部操作。

# 6、输出结果分析

{% pdf  https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/bp神经网络分类_种类_苯酚_类黄酮.pdf %}
```python
# 代码复制成功后，可直接在客户端NoteBook模块中粘贴代码并运行。 
注意：
（1）以上代码对应的数据为案例数据，可自行修改数据来完成算法运算；
（2）只支持spsspro客户端的notebook上调用；
（3）首次安装客户端后，网络良好的情况下，spsspro算法SDK一般一两分钟内会下载完毕。
import numpy
import pandas
from spsspro.algorithm import supervised_learning
#生成案例数据
data_x = pandas.DataFrame({
    "A": numpy.random.random(size=100),
    "B": numpy.random.random(size=100)
})
data_y = pandas.Series(data=numpy.random.choice([1, 2], size=100), name="C")
#BP神经网络分类，输入参数详细可以光标放置函数括号内按shift+tab查看，输出结果参考spsspro模板分析报告
result = supervised_learning.mlp_classifier(data_x=data_x, data_y=data_y)
print(result)
```