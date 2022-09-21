---
title: matlab画图手册（使用PlotPub）
date: 2022-09-16 13:14:16
tags: [数据建模,matlab,画图]
categories: [数据建模,matlab,画图]
swiper: true # 将文章放入轮播图中
---

# PlotPub安装
## 简介
PlotPub 是一个免费和开放源的MATLAB绘图库，用于生成MATLAB漂亮的，出版质量的图。从名字可以看出，该工具包主要是plot绘制一些曲线。

## 下载安装
下载：https://github.com/masumhabib/PlotPub
安装：
```
addpath('/Applications/MATLAB_R2021b.app/toolbox/plotpub');
```
解压后将路径添加到Matlab的环境中即可。
去除路径
```
rmpath('/Applications/MATLAB_R2021b.app/toolbox/plotpub');
```
### 使用手册
http://masumhabib.com/projects/publication-quality-graphs-matlab/plotpub-v2-0-documentation/
## example

```matlab
clear all;

%% lets plot 3 cycles of 50Hz AC voltage
f = 50; % frequency
Vm = 10; % peak
phi = 0; % phase

% generate the signal
t = [0:0.0001:3/f];
th = 2*pi*f*t;
v = Vm*sin(th+phi);

% plot it
figure;
plot(t*1E3, v);
% change settings
plt = Plot(); % create a Plot object and grab the current figure

plt.XLabel = 'Time, t (ms)'; % xlabel
plt.YLabel = 'Voltage, V (V)'; %ylabel
plt.Title = 'Voltage as a function of time'; % plot title
% Save? comment the following line if you do not want to save
plt.Colors = {[0, 0, 0]}; % [red, green, blue]
plt.LineWidth = 2; % line width
plt.LineStyle = {'--'}; % line style: '-', ':', '--' etc
plt.export('plotSimple1.png');



```
其中，f是频率，Vm是峰值电压，t是时间，v是交流电压信号。图非常难看
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-16%2013.52.39.png)

加了这个会变好看
```

%% plot now
opt.XLabel = 'X坐标名称'; % x坐标名字
opt.YLabel = 'y坐标名称'; %yl坐标名字
opt.XLim = [0, 200]; % X坐标区间
opt.YLim = [0, 16]; % y坐标区间
opt.Colors = [1, 0, 0;
    0,1,0] % [red, green, blue](线条颜色)
opt.LineWidth = [2,2]; % 线条宽度
opt.LineStyle = {'-', '--'}; % 线条格式 '-', ':', '--' etc
opt.Legend = {'\theta = 0^o', '\theta = 45^o'}; % 右上角图例

% 保存在文件目录下
opt.FileName = 'plotAxisLimit.jpg'; 

% 创建plot对象
setPlotProp(opt);


```
或者
```matlab
plt = Plot(); % create a Plot object and grab the current figure

plt.XLabel = 'x名称'; % xlabel
plt.YLabel = 'y名称'; %ylabel
plt.Title = '图标title'; % plot title
% Save? comment the following line if you do not want to save
plt.Colors = {[1, 0, 0];[0,1,1]};% [red, green, blue](线条颜色)
plt.LineWidth = 2; % line width
plt.LineStyle = {'--'}; % line style: '-', ':', '--' etc
plt.export('1.png');

```

{% title h1, 二维曲线 %}

```matlab
clear;clc;close all;
x = linspace(1, 200, 100);%均匀生成数字1~200，共计100个
y1 = log(x) + 1;%生成函数y=log(x)+1
y2 = log(x) + 2;%生成函数y=log(x)+2
figure;
plot(x, y1);%作图 y=log(x)+1
hold on %多图共存在一个窗口上
plot(x, y2, 'LineWidth', 2);%%作图 y=log(x)+2，LineWidth指线型的宽度，粗细尺寸2 hold off %关闭多图共存在一个窗口上
legend('y1', 'y2');%生成图例 y1和y2
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/1.png)


{% title h1, 二维散点图 %}
常用来比较理论数据和实验数据的趋势关系;
```matlab
clear;clc;close all;

x = linspace(1, 200, 100);%均匀生成数字1~200，共计100个
y1 = log(x) + 1;%生成函数y=log(x)+1
figure;
y3 = y1 + rand(1, 100) - 0.5;
plot(x, y1, 'LineWidth', 2, 'Color', [0.21, 0.21, 0.67]);
hold on
% 设置数据点的形状、数据点的填充颜色、数据点的轮廓颜色
plot(x, y3, 'o', 'LineWidth', 2, 'Color', [0.46, 0.63, 0.90], 'MarkerFaceColor', [0.35, 0.90, 0.89], 'MarkerEdgeColor', [0.18, 0.62, 0.17]);
hold off
plt = Plot(); % create a Plot object and grab the current figure
plt = Plot(); % create a Plot object and grab the current figure

plt.XLabel = 'x名称'; % xlabel
plt.YLabel = 'y名称'; %ylabel
plt.Title = '图标title'; % plot title
% Save? comment the following line if you do not want to save
plt.Colors = {[1, 0, 0];[0,1,1]};% [red, green, blue](线条颜色)
plt.LineWidth = 2; % line width
plt.LineStyle = {'--'}; % line style: '-', ':', '--' etc
plt.export('2.png');


```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/2.png)

MarkerFaceColor用于设置内部填充颜色
MarkerEdgeColor用于设置外部边框颜色 

{% title h1, 二维渐变图 %}


用不同的颜色、数据点大小表征不同数值，更加直观;
```matlab
x = linspace(0,3*pi,200);
y = cos(x) + rand(1,200);%随机生成1*200，位于[0,1]的数字 
sz = 25;%尺寸为25
c = linspace(1,10,length(x));
scatter(x,y,sz,c,'filled')
```
 linspace - 生成线性间距向量
    此 MATLAB 函数 返回包含 x1 和 x2 之间的 100 个等间距点的行向量。
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/3.png)

- scatter函数用法
1. scatter(x,y) 在向量 x 和 y 指定的位置创建一个包含圆形标记的散点图。
2. 要绘制一组坐标，请将 x 和 y 指定为等长向量。
3. 要在同一组坐标区上绘制多组坐标，请将 x 或 y 中的至少一个指定为矩阵。
4. scatter(x,y,sz) 指定圆大小。要对所有圆使用相同的大小，请将 sz 指定为标量。 要绘制不同大小的每个圆，请将 sz 指定为向量或矩阵。
5. scatter(x,y,sz,c) 指定圆颜色。您可以为所有圆指定一种颜色，也可以更改颜色。 例如，您可以通过将 c 指定为 'red' 来绘制所有红色圆。
6. scatter(___,'filled') 填充圆。可以将 'filled' 选项与前面语法中的任何输入 参数组合一起使用。


{% title h1, 条形图 %}
```matlab
A=[60.689;87.714;143.1;267.9515]; 
C=[127.5;160.4;231.9;400.2]
B=C-A;
D=[A,B,C];
bar1=bar([2:5:17],A,'BarWidth',0.2,'FaceColor','r');
hold on;
bar2=bar([3:5:18],B,'BarWidth',0.2,'FaceColor','y'); 
hold on;
bar3=bar([4:5:19],C,'BarWidth',0.2,'FaceColor','b');
ylabel('耗时/s')
xlabel('GMM阶数')
legend('训练耗时','测试耗时','总耗时');
labelID ={ '8阶','16阶','32阶','64阶'}
set(gca,'XTick',3:5:20);
set(gca,'XTickLabel',labelID)
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/4.png)

 bar - 条形图
    此 MATLAB 函数 创建一个条形图，y 中的每个元素对应一个条形。如果 y 是 m×n 矩阵，则
    bar 创建每组包含 n 个条形的 m 个组。
 set - 设置图形对象属性
    此 MATLAB 函数 为 H 标识的对象指定其 Name 属性的值。使用时须用单引号将属性名引起
    来，例如，set(H,'Color','red')。如果 H 是对象的向量，则 set 会为所有对象设置属
    性。如果 H 为空（即 []），set 不执行任何操作，但不返回错误或警告。

{% title h1, 填充图 %}
```matlab
x = 0.4:0.1:2*pi;
y1 = sin(2*x);
y2 = sin(x);
% 确定 y1 和 y2 的上下边界 
maxY = max([y1; y2]);
minY = min([y1; y2]);
% 确定填充多边形，按照顺时针方向来确定点 
% fliplr 实现左右翻转
xFill = [x, fliplr(x)];
yFill = [maxY, fliplr(minY)];
figure
fill(xFill, yFill, [0.21, 0.21, 0.67]);
hold on
% 绘制轮廓线
plot(x, y1, 'k', 'LineWidth', 2)
plot(x, y2, 'k', 'LineWidth', 2)
hold off
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/5.png)

 fliplr - 将数组从左向右翻转
    此 MATLAB 函数 返回 A，围绕垂直轴按左右方向翻转其各列。

{% title h1, 多Y轴图 %}
```matlab
figure;
load('accidents.mat','hwydata')
ind = 1:51;
drivers = hwydata(:,5);
yyaxis left
scatter(ind, drivers, 'LineWidth', 2);
title('Highway Data');
xlabel('States');
ylabel('Licensed Drivers (thousands)');
pop = hwydata(:,7);
yyaxis right
scatter(ind, pop, 'LineWidth', 2);
ylabel('Vehicle Miles Traveled (millions)');
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/截屏2022-09-16%2015.39.22.png)

{% title h1, 二维场图 %}
```matlab
[x, y] = meshgrid(0:0.1:1, 0:0.1:1);
u=x;
v=-y;
startx = 0.1:0.1:0.9;
starty = ones(size(startx));
% 需要获取所有流线的属性
figure;
quiver(x, y, u, v);%该函数使用箭头来直观的显示矢量场。该调用格式表示通过在(x, y)指定的位置绘制 小箭头来表示以该点为起点的向量(u,v)
streamline(x, y, u, v, startx, starty);
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/6.png)

 meshgrid - 二维和三维网格
    此 MATLAB 函数 基于向量 x 和 y 中包含的坐标返回二维网格坐标。X 是一个矩阵，每一行是
    x 的一个副本；Y 也是一个矩阵，每一列是 y 的一个副本。坐标 X 和 Y 表示的网格有
    length(y) 个行和 length(x) 个列。

 quiver - 箭头图或向量图
    此 MATLAB 函数 在由 X 和 Y 指定的笛卡尔坐标上绘制具有定向分量 U 和 V 的箭头。例
    如，第一个箭头源于点 X(1) 和 Y(1)，按 U(1) 水平延伸，按 V(1) 垂直延伸。默认情况
    下，quiver 函数缩放箭头长度，使其不重叠。

 streamline - 根据二维或三维向量数据绘制流线图
    此 MATLAB 函数 根据三维向量数据 U、V 和 W 绘制流线图。

{% title h1,  三维曲线图 %}

```matlab
 figure;
 t = 0:pi/20:10*pi;
 xt = sin(t);
 yt = cos(t);
 plot3(xt, yt, t, '-o', 'Color', 'b', 'MarkerSize', 10);
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/7.png)

{% title h1, 三维条形图 %}
```matlab
figure;
 x = -20:10:20;
 y=0:100;
 % 随便生成的 5 组数据，也就是目标图上的 5 条曲线数据
 z = zeros(5, 101);
 z(1, 1:10:end) = linspace(1, 10, 11);
 z(2, 1:10:end) = linspace(1, 20, 11);
 z(3, 1:10:end) = linspace(1, 5, 11);
 z(4, 5:10:end) = linspace(1, 10, 10);
 z(5, 80:2:end) = linspace(1, 5, 11);
 fori=1:5
 % x 方向每条曲线都是一个值，重复 y 的长度这么多次
 xx = x(i)*ones(1, 101);
 % z 方向的值，每次取一条
 zz = z(i, :);
 % plot3 在 xyz 空间绘制曲线，保证 x y z 长度一致即可
 plot3(xx, y, zz, 'LineWidth', 2);
 hold on
 end
 hold off
 legend('line1', 'line2', 'line3', 'line4', 'line5');
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/8.png)

{% title h1, 三维散点图 %}
```matlab
clear;clc;close all;
figure;
[X,Y,Z] = sphere(16);
x = [0.5*X(:); 0.75*X(:); X(:)];
y = [0.5*Y(:); 0.75*Y(:); Y(:)];
z = [0.5*Z(:); 0.75*Z(:); Z(:)];
S = repmat([70, 50, 20],numel(X), 1); 
C = repmat([1, 2, 3], numel(X), 1); 
s=S(:);
c=C(:);
h = scatter3(x, y, z, s, c);
h.MarkerFaceColor = [0 0.5 0.5];
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/9.png)

 repmat - 重复数组副本
    此 MATLAB 函数 返回一个数组，该数组在其行维度和列维度包含 A 的 n 个副本。A 为矩阵
    时，B 大小为 size(A)*n。

 scatter3 - 三维散点图
    此 MATLAB 函数 在向量 X、Y 和 Z 指定的位置显示圆圈。



```matlab
clear;clc;close all;
x = linspace(1, 200, 100); 
y1 = log(x) + 1;
y2 = log(x) + 2;
y3 = y1 + rand(1, 100) - 0.5; 
figure;
scatter3(x, y2, y3, x, x, 'filled');
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/10.png)

 linspace - 生成线性间距向量
    此 MATLAB 函数 返回包含 x1 和 x2 之间的 100 个等间距点的行向量。



{% title h1, 三维伪彩图 %}

```matlab
[x, y, z] = peaks(30);
figure;
plot1 = subplot(1,2,1);
surf(x, y, z);
colormap();
% 获取第一幅图的 colormap，默认为 parula  
plot2 = subplot(1,2,2);
surf(x, y, z);
% 下面设置的是第二幅图的颜色
colormap(hot);

```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/12.png)

 colormap - 查看并设置当前颜色图
    此 MATLAB 函数 将当前图窗的颜色图设置为预定义的颜色图之一。如果您为图窗设置了颜色
    图，图窗中的坐标区和图将使用相同的颜色图。新颜色图的长度（颜色数）与当前颜色图相同。当您
    使用此语法时，不能为颜色图指定自定义长度。有关颜色图的详细信息，请参阅什么是颜色图？。

 subplot - 在各个分块位置创建坐标区
    此 MATLAB 函数 将当前图窗划分为 m×n 网格，并在 p 指定的位置创建坐标区。MATLAB 按行
    号对子图位置进行编号。第一个子图是第一行的第一列，第二个子图是第一行的第二列，依此类
    推。如果指定的位置已存在坐标区，则此命令会将该坐标区设为当前坐标区。



```matlab
% 一个坐标轴
figure;
h1 = surf(x, y, z);
hold on
h2 = surf(x, y, z + 5); 
hold off
colormap();
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/13.png)

{% title h1, 裁剪伪彩图 %}
```matlab
clear;clc;close all;
figure;
n=300;
[x, y, z] = peaks(n);
subplot(2, 2, [1,3])
surf(x, y, z);
shading interp
view(0, 90)
for i=1:n
    for j=1:n
        if x(i,j)^2+2*y(i,j)^2>6&&2*x(i,j)^2+y(i,j)^2<6
            z(i, j) = NaN;
        end
    end
end
subplot(2, 2, 2)
surf(x, y, z);
shading interp
view(0, 90)
subplot(2, 2, 4)
surf(x, y, z);
shading interp
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/14.png)



 peaks - peaks 函数
    此 MATLAB 函数 返回在一个 49×49 网格上计算的 peaks 函数的 z 坐标。

 surf - 曲面图
    此 MATLAB 函数 创建一个三维曲面图，它是一个具有实色边和实色面的三维曲面。该函数将矩阵
    Z 中的值绘制为由 X 和 Y 定义的 x-y 平面中的网格上方的高度。曲面的颜色根据 Z 指定的高
    度而变化。

 shading - 设置颜色着色属性
    此 MATLAB 函数 每个网格线段和面具有恒定颜色，该颜色由该线段的端点或该面的角边处具有最
    小索引的颜色值确定。

 view - 相机视线
    此 MATLAB 函数 为当前坐标区设置相机视线的方位角和仰角。



{% title h1, 等高线图 %}
```matlab
clear;clc;close all;
figure;
[X, Y, Z] = peaks;
subplot(2, 2, 1);
contour(X, Y, Z, 20, 'LineWidth', 2);
subplot(2, 2, 2);
contour(X, Y, Z, '--', 'LineWidth', 2)
subplot(2, 2, 3);
v =[1,1];
contour(X, Y, Z, v, 'LineWidth', 2);
x = -2:0.2:2;
y = -2:0.2:3;
[X, Y] = meshgrid(x, y);
Z = X.*exp(-X.^2-Y.^2);
subplot(2, 2, 4);
contour(X, Y, Z, 'ShowText','on', 'LineWidth', 2);
```

![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/15.png)


 contour - 矩阵的等高线图
    此 MATLAB 函数 创建一个包含矩阵 Z 的等值线的等高线图，其中 Z 包含 x-y 平面上的高度
    值。MATLAB 会自动选择要显示的等高线。Z 的列和行索引分别是平面中的 x 和 y 坐标。
 figure - 创建图窗窗口
    此 MATLAB 函数 使用默认属性值创建一个新的图窗窗口。生成的图窗为当前图窗。
 meshgrid - 二维和三维网格
    此 MATLAB 函数 基于向量 x 和 y 中包含的坐标返回二维网格坐标。X 是一个矩阵，每一行是
    x 的一个副本；Y 也是一个矩阵，每一列是 y 的一个副本。坐标 X 和 Y 表示的网格有
    length(y) 个行和 length(x) 个列。



{% title h1, 三维等高线图 %}

```matlab
clear;clc;close all;
figure('Position', [0, 0, 900, 400]); 
subplot(1, 3, 1);
[X, Y, Z] = sphere(50);
contour3(X, Y, Z, 'LineWidth', 2); 
[X, Y] = meshgrid(-2:0.25:2);
Z = X.*exp(-X.^2-Y.^2);
subplot(1, 3, 2);
contour3(X, Y, Z, [-0.2 -0.1 0.1 0.2], 'ShowText', 'on', 'LineWidth', 2)
[X, Y, Z] = peaks;
subplot(1, 3, 3);
contour3(X, Y, Z, [2 2], 'LineWidth', 2);
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/17.png)



{% title h1, 等高线填充图 %}

```matlab
clear;clc;close all;
figure;
subplot(2, 2, 1);
[X, Y, Z] = peaks(50);
contourf(X, Y, Z);
subplot(2, 2, 2);
contourf(X, Y, Z,'--');
% 限定范围
subplot(2, 2, 3);
contourf(X, Y, Z, [2 3], 'ShowText', 'on'); 
subplot(2, 2, 4);
contourf(X, Y, Z,[2 2]);
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/16.png)

 contourf - 填充的二维等高线图
    此 MATLAB 函数 创建一个包含矩阵 Z 的等值线的填充等高线图，其中 Z 包含 x-y 平面上的高
    度值。MATLAB 会自动选择要显示的等高线。Z 的列和行索引分别是平面中的 x 和 y 坐标。


{% title h1, 三维矢量场图 %}
```matlab
clear;clc;close all;
figure;
[X, Y, Z] = peaks(30);
% 矢量场，曲面法线
[U, V, W] = surfnorm(X, Y, Z);
% 箭头长度、颜色
quiver3(X, Y, Z, U, V, W, 0.5, 'r');  
hold on
surf(X,Y,Z);
xlim([-3, 3]);
ylim([-3, 3.2]);
shading interp
hold off
view(0, 90);
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/18.png)



{% title h1, 伪彩图+投影图 %}
```matlab
clear;clc;close all;
clear;clc;close all;
x = linspace(-3, 3, 30);
y = linspace(-4, 4, 40);
[X, Y] = meshgrid(x, y);
Z = peaks(X, Y);
Z(5:10, 15:20) = 0;
z1 = max(Z);
z2 = max(Z, [], 2);
figure;
subplot(3, 3, [1, 2]);
plot(x, z1, 'LineWidth', 2); 
subplot(3, 3, [6, 9]);
plot(z2, y, 'LineWidth', 2); 
subplot(3, 3, [4, 5, 7, 8]);
surf(x, y, Z);
xlim([-3, 3]);
ylim([-4, 4]);
view(0, 90);
shading interp%平滑图像
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/19.png)


{% title h1, 热图 %}
```matlab
clear;clc;close all;
clear;clc;
z = rand(50);
z(z>=0.0&z<0.6)=0.5;
z(z>=0.6&z<0.8)=0.7;
z(z>=0.8&z<=1)=0.9;
for i=1:30
    z(randi(50, 1, 1) : end, i) = nan;
end 
for i=31:50
    z(30 + randi(20, 1, 1) : end, i) = nan;
end
z(20:25, 40:45) = nan;
figure;
% ax = surf(z);
ax = pcolor(z);
view(0, 90);
ax.EdgeColor = [1 1 1];
```
![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/20.png)



{% title h1, 热力图 %}

```matlab
clear
X=randn(8000,1);
Y=randn(8000,1);
Xmin=min(X);Xmax=max(X);
Ymin=min(Y);Ymax=max(Y);


% t=[0:0.001:1].^1.0;
% X=0.5*(t).*cos(618*pi*t)+0.5;
% Y=0.5*(t).*sin(618*pi*t)+0.5;
% Xmin=0;Xmax=1;Ymin=0;Ymax=1;

%加密划分区间
Nx=500;
Ny=500;

Xedge=linspace(Xmin,Xmax,Nx);
Yedge=linspace(Ymin,Ymax,Ny);

%N的xy定义是转置的
[N,~,~,binX,binY] = histcounts2(X,Y,[-inf,Xedge(2:end-1),inf],[-inf,Yedge(2:end-1),inf]);

XedgeM=movsum(Xedge,2)/2;
YedgeM=movsum(Yedge,2)/2;

[Xedgemesh,Yedgemesh]=meshgrid(XedgeM(2:end),YedgeM(2:end));

%绘制pcolor图
figure(1)
pcolor(Xedgemesh,Yedgemesh,N');shading interp

%滤波平滑
%h=ones(round(Nx/20));
%h=fspecial('disk',round(Nx/40));
h = fspecial('gaussian',round(Nx/20),6);%最终选用高斯滤波
N2=imfilter(N,h);
figure(2)
pcolor(Xedgemesh,Yedgemesh,N2');shading interp

ind = sub2ind(size(N2),binX,binY);
col = N2(ind);

figure(3)
scatter(X,Y,20,col,'filled');



```

[热力图](https://www.freesion.com/article/46711092993/)

![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/21.png)![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/22.png)

 ![](https://cdn.jsdelivr.net/gh/innocabroad/imageRepository/img/23.png)

heatmap - 创建热图
    此 MATLAB 函数 基于表 tbl 创建一个热图。xvar 输入参数指示沿 x 轴显示的表变量。yvar
    输入参数指示沿 y 轴显示的表变量。默认颜色基于计数聚合，这种方法计算每对 x 和 y 值一起
    出现在表中的总次数。


