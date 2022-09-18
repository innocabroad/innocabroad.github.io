---
title: markdown使用手册
date: 2022-09-13 12:17:18
tags: markdown
categories: 使用手册
---
# 标题

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

### 书写方法：



```markdown
 # 一级标题
 ## 二级标题
 ### 三级标题
 #### 四级标题
 ##### 五级标题
 ###### 六级标题
```

> 注意每一组 # 号与后面文字之间是有一个空格的距离的，对应的是html语法中,标题的 h1~ h6 ，字号从大到小，h1 为最大字号标题，所以使用了一个 # 号，以此类推，话不多说。

------

## 字体样式

**文字加粗**
*我是斜体*

## 书写方法：



```markdown
**文字加粗**
*我是斜体*
```

> 这里的*号和文字之间是没有那一个空格的

------

## 链接

[我是简书首页](https://www.jianshu.com/u/76248a08aa28)

### 书写方法



```markdown
[我是简书首页](https://www.jianshu.com/u/76248a08aa28)
```

> [我是简书链接] 是页面上看见的内容，([https://www.jianshu.com](https://www.jianshu.com/))这个是看不到，是给文字添加的链接

------

## 无序列表

- 无序列表1
- 无序列表2
- 无序列表3

## 书写方法



```markdown
- 无序列表1
- 无序列表2
- 无序列表3
```

> 这里的是短横线-，就是=等于号左边的按键，注意-与文字之间有一个空格的距离。

### 在无序列表中还可以有二级以及三级列表

- 无序列表1
  - 二级无序列表1
  - 二级无序列表2
    - 三级无序列表1
    - 三级无序列表2
- 无序列表2
- 无序列表3

## 书写方法



```markdown
- 无序列表1
  - 二级无序列表1
  - 二级无序列表2
    - 三级无序列表1
    - 三级无序列表2
- 无序列表2
- 无序列表3
```

> 一级列表是： - + 一个空格 + 加文字，这样的写法，那么二级，三级也是这样的写法，只是在二级列表的短横线前面，需要按一下Tab键，你会看到光标向右缩进了，这时候就是二级列表的位置，当然必须在一级列表的下一行。三级就是按两下Tab键，而且必须在二级列表的下一行，如下：



```markdown
-(空格)无序列表1
(Tab)-(空格)二级无序列表1
(Tab)(Tab)-(空格)三级无序列表1
```

------

## 有序列表：

1. 有序列表1
2. 有序列表2
3. 有序列表3

## 书写方法



```markdown
1. 有序列表1
2. 有序列表2
3. 有序列表3
```

------

## 表格:

| 表格1 | 表格2 |
| :---: | :---: |
| 内容1 | 内容2 |
| 内容3 | 内容4 |

### 书写方法



```markdown
|表格1|表格2|
|:-:|:-:|
|内容1|内容2|
|内容3|内容4|
```

> |:-:| 这是一列表格，|:-:|:-:|这里两列表格，嗯。。。以此类推，几列就写几个，固定写法。当然文字与符号之间加空格，或者多加几个短横线都是没问题的。

------

## 辅助内容：

> 这是引入文字

### 书写方法



```markdown
>这是引入文字
```

## 一根横线：

------

------

### 书写方法



```markdown
---或者***
```

------

## 删除线:

~~这是删除线~~

### 书写方法



```markdown
~~这是删除线~~
```

------

## 特殊标记：

```markdown
特殊标记
```

### 书写方法



```markdown
`特殊标记`
```

> 注意：不是单引号，不是单引号，不是单引号！是英文状态下的Tab键上面的那个按钮

------

## 代码块区域：



```markdown
  <script>
    document.write('abc');
  </script>
```

### 书写方法



```markdown
  >```
  >  <script>
  >    document.write('abc');
  >  </script>
  >```
```

> **注意：** 这里面的>这五个只是为了不让代码生效，在写代码块区域的时候不需要写，写法是去掉>这五个之后剩下的内容。这六个小点()也是英文状态下的Tab键上面的那个按钮。



## 修改字体颜色：

大家最为关注的应该是如何更改 
```markdown
<big>![\color{red}{字体颜色}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7B%E5%AD%97%E4%BD%93%E9%A2%9C%E8%89%B2%7D)</big> 吧。
```

### 无效写法



```markdown
<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=red>我是红色</font>
<font color=#008000>我是绿色</font>
<font color=Blue>我是蓝色</font>
<font size=5>我是尺寸</font>
<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>
```

### 正确方法



```markdown
$\color{red}{字体颜色}$
或者
$\color{#FF0000}{红色字}$或$\color{rgb(255,0,0)}{红色字}$
```

> **注意** 在一般markdown编辑器中有效的，但在简书中无效的功能有TOC , 注释和阅读更多, MathJax, 顺序图或流程图,任务列表（Task lists）。

## 插入图片

{% asset_img test1.jpg 图片引用方法一 %}

在生成的对应文件夹放入图片命名即可


## 预览pdf
### 第一种方法使用 embed标签，这是html自带的，例如：
<embed src="https://huiyan.baidu.com/cms/2017%E5%B9%B4%E7%AC%AC%E4%B8%80%E5%AD%A3%E5%BA%A6%E4%B8%AD%E5%9B%BD%E5%9F%8E%E5%B8%82%E7%A0%94%E7%A9%B6%E6%8A%A5%E5%91%8A.pdf" type="application/pdf" width=100% height=500>

### 书写方法

```markdown
<embed src="https://huiyan.baidu.com/cms/2017%E5%B9%B4%E7%AC%AC%E4%B8%80%E5%AD%A3%E5%BA%A6%E4%B8%AD%E5%9B%BD%E5%9F%8E%E5%B8%82%E7%A0%94%E7%A9%B6%E6%8A%A5%E5%91%8A.pdf" type="application/pdf" width=100% height=500>
```
后面的width和height代表宽度和高度

### 第二种方法，使用hexo的一个插件hexo-pdf
首先安装插件

npm install --save hexo-pdf
然后在.md文件中写入如下代码

{% pdf  https://huiyan.baidu.com/cms/2017%E5%B9%B4%E7%AC%AC%E4%B8%80%E5%AD%A3%E5%BA%A6%E4%B8%AD%E5%9B%BD%E5%9F%8E%E5%B8%82%E7%A0%94%E7%A9%B6%E6%8A%A5%E5%91%8A.pdf %}

### 书写方法


```markdown
{% pdf  https://huiyan.baidu.com/cms/2017%E5%B9%B4%E7%AC%AC%E4%B8%80%E5%AD%A3%E5%BA%A6%E4%B8%AD%E5%9B%BD%E5%9F%8E%E5%B8%82%E7%A0%94%E7%A9%B6%E6%8A%A5%E5%91%8A.pdf %}

```
### 本地pdf上传

> 可以用本地的，例如在source文件夹下创建一个pdf文件夹，然后把test.pdf放进去，最后在.md文件中这样写就行了


### 书写方式

```markdown

<embed src="/pdf/test.pdf" type="application/pdf" width=100% height=500>
{% pdf  /pdf/test.pdf %}
```

## Markdown 链接

这是一个链接 [菜鸟教程](https://www.runoob.com)

```markdown
这是一个链接 [菜鸟教程](https://www.runoob.com)
```
