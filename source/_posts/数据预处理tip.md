---
title: 数据预处理tip
date: 2022-09-16 19:53:49
tags: [数学建模] 
categories: [数学建模] 
swiper: true # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/006VlWHuly1h45cmx9epqj31zj2za1l5.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/006VlWHuly1h45cmx9epqj31zj2za1l5.jpg' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: false
---
优秀论文怎么写？？？

## 数据分析&预处理
附件？给出了在多个地点采集得到的?组数据，每组文件包含了在同一地点采集到的多个数据，其中有干扰和无干扰情况下各?组。由于实际测量过程中的误差，本题须对原始记录进行数据提取及预处理操作，并删除掉其中的一些“无用”样本，主要考虑异常、缺失、相同或相似4种情况，再经过[卡尔曼滤波](https://baike.baidu.com/item/卡尔曼滤波?fromModule=lemma_search-box)用于之后的建模研究。总体的数据处理流程如下图 3-1 所示。
```mermaid
A[样本数据] –>B[正则表达式提取] 
B->C[剔除时间戳缺失样本] 
C–>D[删除相同样本] 
D–>E[相似变量选择] 
E–>F[拉依达准则去除异常值] 
F–>G[样本确定]
```
总体处理步骤分为 5 步，首先基于原始数据格式，采用正则表达式抓取其中的可用数据，按照每4 行保存成一个样本的保存要求得到原始数据集1;再判断同一时间戳是否采集到了完整的4个锚点测距值，剔除掉其中有缺失和完全重复的样本，得到数据集2;之后分析测量值与校验值等变量的相关性实现关键特征变量的选取，删除不必要的变量列;然后采用拉依达准则(3σ准则)去除误差较大的异常值，得到数据集3;最后以二维表形式展示最终的数据预处理结果。

[拉依达准则](https://baike.baidu.com/item/拉依达准则/5678473)
> 拉依达准则是指先假设一组检测数据只含有随机误差，对其进行计算处理得到标准偏差，按一定概率确定一个区间，认为凡超过这个区间的误差，就不属于随机误差而是粗大误差，含有该误差的数据应予以剔除。这种判别处理原理及方法仅局限于对正态或近似正态分布的样本数据处理，它是以测量次数充分大为前提的，当测量次数少的情形用准则剔除粗大误差是不够可靠的。因此，在测量次数较少的情况下，最好不要选用该准则。

## 数据处理
1. 附件1为实际场景下测得的数据，主要包括无干扰的正常数据、有干扰的异常数据以及对应的Tag坐标信息。其中Tag信息为标准的结构化数据格式,不需要再做额外的处理，具体格式如表所示(表 3-1 三维 Tag 坐标数据信息格式)
有无干扰下的正常/异常样本数据则由结构化数字和非结构化文本共同构成，因此需要进一步的数据提取和处理。其中须重点列出的第24个Tag的正常样本数据和第1个Tag的异常样本数据格式具体如表3-2所示。T表示时间戳，即数据采集的时刻;PR表示4个锚点的ID标号;4 列数据分别对应该锚点的测距值(mm):测距值的校验值:数据序列号:数据编号;每4行为1组代表了UWB采集到的一组完整数据。
> 描述数据 数据构成 字母代表含义
2. 正则表达式提取数据
附件 1 中 648 组样本数据均为如表 3-2 所示的非结构化数据格式，故需设计一种 文本匹配模式以抓取出其中关键的结构化数据，再用于之后数据的处理和建模。本题 采用正则表达式来得到时间戳、锚点标号、对应测距值、对应校验值这 4 列关键数据， 针对每个txt文本进行遍历(正常/异常样本分开处理)，若存在以下格式:
```
Compile = r'T:(\w+):RR:0:(\w+):(\w+):(\w+)' 
```
则抽取出相应位置的数值形成一条结构化数据，之后将相同时间戳的 4 个锚点测距值 和校验值合并为一个样本数据，再与 Tag 标签信息进行整合，形成初始的正常样本和 异常样本。其中 Compile 表示数据匹配模板，\w+表示匹配单词字符及数字。

## 缺失数据的处理

由于同一时间戳的4个锚点数据才为一组完整的数据，此部分数据处理工作需结合正则表达式提取出来的时间戳标识进行。首先分别遍历正常样本和异常样本txt文件，利用正则表达式匹配出关键数据,再统计样本中每个时间戳的频次，若存在Counter(Ti ) <4
则认为该时间戳数据缺失，但由于实际测量得到的数值本身存在着不同程度的误差，再进行补全将可能引入更加复杂的误差，且数据样本足够用来之后的建模工作，故我们不考虑这类缺失数据的补全，直接将该时间戳的数据剔除。(原因)
## 相同数据的剔除

缺失数据处理完后，将同一时间戳的四个锚点数据整合成一个样本，即每个样本对应1个时间戳和8个距离数据，再进行相同数据的剔除。首先因测距值和校验值完全相同，我们将4列校验值全部删除，只将4列测距值作为模型输入;再进行每行样 本的遍历比较，剔除掉相同的样本数据;最后处理得到的测距数据再与对应的Tag坐标信息进行整合形成数据集2。
## 异常数据的剔除
针对正常样本和异常样本中可能存在的异常值，本文选用拉依达准则(又称 3 准 则)对数据集进行检验。假设测量得到 4 个测距值 m1 , m2 , m3 , m4 为等精度测量，可计 算出其算术平均值m以及剩余误差
若为该行样本是含有粗大误差的异常值，应予剔除。例如正常样本中第 24 个 Tag 位置 以及第 109 个 Tag 位置数据的剔除情况如下图 3-2、3-3 所示。

至此，“无用”数据(缺失、相同、相似、异常)的预处理过程完毕。按照上述过程的处理结果如表 3-3 所示，具体数据结果见上传的附件 1-“第一问数据处理”。
```matlab
clear
clc
%% 根据拉依达准则对二维数据进行筛选
mat= xlsread('陕西灌流器.xlsx','data','A2:W55'); %读取数据
% ave_all=[];
% sigma_all=[];
sizes=size(mat);
for j=1:sizes(2)    
    ave(j) = mean(mat(:,j));%mean 求解平均值
    %ave_all=[ave_all,ave(j)];
    sigma(j) = std(mat(:,j));%求解标准差
    sigma(j)
    %sigma_all=[sigma_all,sigma(j)];
    for i = 1:sizes(1)
        if(abs(mat(i,j)-ave(j))>3*sigma(j));%不符合3σ准则,标记这个元素位置
            disp(['第',num2str(i),'行','第',num2str(j),'列,出现不满足拉依达准则的数据，数据id为：'])
            data_id=mat(i,1) %%如果以actxserver读取的话,这里可以设置excel中单元格格式
            mat(i,j)=-1;%% 这里用数据中没出现过的-1来替代待剔除的值
        else
            continue;
        end
    end
end




```

```python
import os
import re
import numpy as np
import pandas as pd
from os import listdir
from collections import Counter
def missing_data_processing(content,j):
a = []
time = re.compile(r'T:(\w+):RR').findall(content) b = list(Counter(time))
for i in b:
if (Counter(time)[i]== 4): a.append(i)
if (int(j)==109): print(len(a))
return a
def three_sigmal(data): n = 3 # n*sigma
print(data)
ymean = np.mean(data, axis=0)
ystd = np.std(data, axis=0) # 标准差 threshold1 = ymean - n * ystd threshold2 = ymean + n * ystd
outlier = [] # 将异常值保存
final = [] # 删除掉异常值后的数据 for i in range(0, len(data)):
#print(np.abs(data[i]-ymean))
if (np.abs(data[i]-ymean) > n * ystd).any() : #
outlier.append(data[i])
else: final.append(data[i])
return outlier
normal_data_path = 'D:/竞赛/数学建模/2021 年 E 题/附件 1:UWB 数据集/正常数据' abnormal_data_path = 'D:/竞赛/数学建模/2021 年 E 题/附件 1:UWB 数据集/异常数 据'
label_path = 'D:/竞赛/数学建模/2021 年 E 题/附件 1:UWB 数据集/Tag 坐标信息.txt' filename1 = listdir(normal_data_path)
filename2 = listdir(abnormal_data_path)
# 均值
filename1.sort(key=lambda x:int(x.split('.')[0])) filename2.sort(key=lambda x:int(x.split('.')[0])) # 整合标签数据
label = []
with open(label_path, encoding='utf-8') as f:
line = f.readline() # 以行的形式进行读取文件 while line:
a = line.split()
b = a[1:4] # 这是选取需要读取的位数 label.append(b) # 将其添加在列表之中 line = f.readline()
f.close()
## 整合正常、异常数据
normal_df = extract_data(normal_data_path,filename1,label) abnormal_df = extract_data(abnormal_data_path,filename2,label) ## 删除重复数据
x1 = normal_df.drop_duplicates()
x2 = abnormal_df.drop_duplicates() print(abnormal_df['measure1'][abnormal_df['filename']==str(100)]) print(x2['measure1'][x2['filename']==str(100)])
```
