---
title: 遗传算法matlab工具箱
date: 2022-09-15 17:49:59
tags: [遗传算法,matlab,数据建模]
categories: [数据建模,遗传算法]
swiper: true # 将文章放入轮播图中
swiperImg: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/src=http---img-blog.csdn.net-20171010005726856&refer=http---img-blog.csdn.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto.webp' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
img: 'https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/src=http---img-blog.csdn.net-20171010005726856&refer=http---img-blog.csdn.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto.webp' # 该文章图片，可以是本地目录下图片也可以是http://xxx图片
top: true
---

# 简介
遗传算法是现代优化算法之一，为方便使用Matlab提供了遗传算法工具箱，可以方便我们解决一般的优化问题。

https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-15%2017.54.27.png

谢菲尔德遗传工具箱的使用
安装[遗传工具箱](https://github.com/UoS-CODeM/GA-Toolbox.git)
1. 先下载谢菲尔德遗传工具箱包，把里面文件夹gatbx复制到matlab安装包toolbox文件夹下，粘贴ok

2. 找到主页点击设置路径，找到matlab安装包toolbox文件夹下的文件夹gatbx
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-15%2019.02.42.png)
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-15%2019.03.49.png)
3.  可以使用函数ver查看gatbx工具箱的名字、发行版本等
```
 v = ver('gatbx')
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-15%2019.06.14.png)

{% titleB h2, 案例一  简单一元函数的优化  %}
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/2ba7adf475e9481e94d1dec1680287de.png)

```matlab



clc
clear all
close all
%% 画出函数图
figure(1);
hold on;
lb=1;ub=2; %函数自变量范围【1,2】
ezplot('sin(10*pi*X)/X',[lb,ub]);   %画出函数曲线
xlabel('自变量/X')
ylabel('函数值/Y')
%% 定义遗传算法参数
NIND=40;        %个体数目
MAXGEN=20;      %最大遗传代数
PRECI=20;       %变量的二进制位数
GGAP=0.95;      %代沟
px=0.7;         %交叉概率
pm=0.01;        %变异概率
trace=zeros(2,MAXGEN);                        %寻优结果的初始值
FieldD=[PRECI;lb;ub;1;0;1;1];                      %区域描述器
Chrom=crtbp(NIND,PRECI);  %创建任意离散随机种群                    
%% 优化
gen=0;                                  %代计数器
X=bs2rv(Chrom,FieldD);                 %计算初始种群的十进制转换
ObjV=sin(10*pi*X)./X;        %计算目标函数值
while gen<MAXGEN
   FitnV=ranking(ObjV);                               %分配适应度值，估算适应度
   SelCh=select('sus',Chrom,FitnV,GGAP);              %选择
   SelCh=recombin('xovsp',SelCh,px);                  %重组
   SelCh=mut(SelCh,pm);                               %变异
   X=bs2rv(SelCh,FieldD);               %子代个体的十进制转换
   ObjVSel=sin(10*pi*X)./X;             %计算子代的目标函数值
   [Chrom,ObjV]=reins(Chrom,SelCh,1,1,ObjV,ObjVSel); %重插入子代到父代，得到新种群
   X=bs2rv(Chrom,FieldD);
   gen=gen+1;                                             %代计数器增加
   %获取每代的最优解及其序号，Y为最优解,I为个体的序号
   [Y,I]=min(ObjV);
   trace(1,gen)=X(I);                            %记下每代的最优值
   trace(2,gen)=Y;                               %记下每代的最优值
end
plot(trace(1,:),trace(2,:),'bo');                            %画出每代的最优点
grid on;
plot(X,ObjV,'b*');   %画出最后一代的种群
hold off
%% 画进化图
figure(2);
plot(1:MAXGEN,trace(2,:));
grid on
xlabel('遗传代数')
ylabel('解的变化')
title('进化过程')
bestY=trace(2,end);
bestX=trace(1,end);
fprintf(['最优解:\nX=',num2str(bestX),'\nY=',num2str(bestY),'\n'])
```
 运行后会输出两张图，左图为目标函数图，图二为进化图
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-15%2019.09.17.png)
>最优解:
X=1.1491
Y=-0.8699

{% titleB h2, 案例二  多元函数优化  %}
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/82d8566fce5340c5948d7632d4c8c2ad.png)
 遗传算法优化程序代码：


```matlab
clc
clear all
close all
%% 画出函数图
figure(1);
lbx=-2;ubx=2; %函数自变量x范围【-2,2】
lby=-2;uby=2; %函数自变量y范围【-2,2】
ezmesh('y*sin(2*pi*x)+x*cos(2*pi*y)',[lbx,ubx,lby,uby],50);   %画出函数曲线
hold on;
%% 定义遗传算法参数
NIND=40;        %个体数目
MAXGEN=50;      %最大遗传代数
PRECI=20;       %变量的二进制位数
GGAP=0.95;      %代沟
px=0.7;         %交叉概率
pm=0.01;        %变异概率
trace=zeros(3,MAXGEN);                        %寻优结果的初始值
FieldD=[PRECI PRECI;lbx lby;ubx uby;1 1;0 0;1 1;1 1];                      %区域描述器
Chrom=crtbp(NIND,PRECI*2);                      %初始种群
%% 优化
gen=0;                                  %代计数器
XY=bs2rv(Chrom,FieldD);                 %计算初始种群的十进制转换
X=XY(:,1);Y=XY(:,2);
ObjV=Y.*sin(2*pi*X)+X.*cos(2*pi*Y);        %计算目标函数值
while gen<MAXGEN
   FitnV=ranking(-ObjV);                              %分配适应度值
   SelCh=select('sus',Chrom,FitnV,GGAP);              %选择
   SelCh=recombin('xovsp',SelCh,px);                  %重组
   SelCh=mut(SelCh,pm);                               %变异
   XY=bs2rv(SelCh,FieldD);               %子代个体的十进制转换
   X=XY(:,1);Y=XY(:,2);
   ObjVSel=Y.*sin(2*pi*X)+X.*cos(2*pi*Y);             %计算子代的目标函数值
   [Chrom,ObjV]=reins(Chrom,SelCh,1,1,ObjV,ObjVSel); %重插入子代到父代，得到新种群
   XY=bs2rv(Chrom,FieldD);
   gen=gen+1;                                             %代计数器增加
   %获取每代的最优解及其序号，Y为最优解,I为个体的序号
   [Y,I]=max(ObjV);
   trace(1:2,gen)=XY(I,:);                       %记下每代的最优值
   trace(3,gen)=Y;                               %记下每代的最优值
end
plot3(trace(1,:),trace(2,:),trace(3,:),'bo');                            %画出每代的最优点
grid on;
plot3(XY(:,1),XY(:,2),ObjV,'bo');  %画出最后一代的种群
hold off
%% 画进化图
figure(2);
plot(1:MAXGEN,trace(3,:));
grid on
xlabel('遗传代数')
ylabel('解的变化')
title('进化过程')
bestZ=trace(3,end);
bestX=trace(1,end);
bestY=trace(2,end);
fprintf(['最优解:\nX=',num2str(bestX),'\nY=',num2str(bestY),'\nZ=',num2str(bestZ),'\n'])
```
 结果展示


![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-15%2019.12.31.png)

 遗传算法工具箱提供了一种求解非线性、多模型、多目标、等复杂系统优化问题的通用框架，它不依赖问题的具体领域，对问题的种类具有很强的鲁棒性，所以它广泛应用于各个科学领域。

> 最优解:
X=-1.7665
Y=1.5151
Z=3.2655

<embed src="https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/《遗传算法及其matlab实现》.pdf" type="application/pdf" width=100% height=500>


查看pdf1
# 优秀论文介绍

遗传算法是 Holland 教授于 1962 年提出的模拟自然界遗传机制和生物进化论 而成的一种并行随机搜索最优化方法。它的基本思想是把生物界“优胜劣汰”的进化原理引入优化参数形成的编码串联群体中，按照所选的适应度函数并通过遗传中的选择、交叉和变异对个体进行筛选，使适应度好的个体被保留，适应度 差的个体被淘汰，新的群体既继承上一代的信息，又优于上一代。这样反复循环，直至满足条件。它的基本步骤如下:

1. 随机初始化种群;
2. 计算种群适应度，从中找出最优个体;
3. 依次进行选择操作、交叉操作和变异操作;
4. 重复验算，达到预定的进化代数时为止。
5. 
遗传算法是模拟自然界生物进化过程与机制求解极值问题的一类自组织、自适应人工智能技术，其基本思想是模拟自然界遗传机制和生物进化论而形成的一种过程搜索最优解的算法，具有坚实的生物学基础。遗传算法提供了一种求解复 杂系统优化问题的通用框架，具有广泛的应用价值。 
# 遗传算法的优缺点

2.1 遗传算法的优点
1) 如果处理得当，可以在优化问题中得到全局最优解
2) 比较容易实现并行化计算
3) 遗传算法以结果为导向，最关注的两个点，一是编码与解码，一是适应度函数。它需要的背景知识少，也不需要太关注过程。所以应用范围非常广，可以解决非线性、不连续的问题，甚至有些无法清晰知道过程的问题，也可以解决。
总之就是原理简单，功效强大。
2.2 遗传算法的缺点
1) 遗传算法非常依赖适应度函数，可以说适应度函数直接确定了结果的走向，而这个函数需要使用者自行提供，而且还没有标准，需根据实现问题总结出来
2) 群体大小选择不当，或者选择压设置不对，都可能会过早收敛，错过全局最优解，只能达到局部最优解
3) 因为遗传算法并不太关注过程，所以计算过程中的参数稍有不同可能会得到不同结果。这些参数包括群体大小、交换频率、突变频率等。
4) 当染色体过长(即基因数过多)时，需要重组的片段更多，导致群体规模非常大，使计算时间急剧增加
