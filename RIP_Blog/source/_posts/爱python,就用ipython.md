---
title: 爱Python, 就用ipython
date: 2020-02-14 19：00：00
categories:
	- 工具
	- Python
tags:
	- Python
	- 工具
excerpt: 推荐一款python神器
---

>本文首发于[vito的CSDN博客](https://blog.csdn.net/weixin_43608722/article/details/104297628)，经作者同意后转载。
---

本人Python爱好者，学习Python半年。一个月前我偶然接触到IPython，收益匪浅，在这里分享给大家

-----------------
### 001.什么是IPython
`IPython`（interactive python），即交互式python，比默认的python shell 好用得多，支持变量自动补全，自动缩进，内置了许多很有用的功能和函数.

使用IPython的方式有两种，`IPython shell`和`jupyter notebook`，本文重点介绍jupyter notebook，IPython 被紧密地连接在Jupyter[(http://jupyter.org)](http://jupyter.org) 项目中.

### 010.为什么选择jupyter notebook
Jupyter Notebook 是 IPython shell 基于浏览器的界面，提供了各种花里胡哨的功能如：内置markdown格式、可视化图像……不仅可以运行python代码，而且作为学习python的笔记本也是不错的选择.你也可以分享你的notebook（*.ipynb文件*），这样你的小伙伴们也可以在自己的电脑上运行你的notebook代码
总而言之，jupyter notebook ==界面友好，功能强大==

### 011.jupyter notebook的安装
jupyter的安装方法有两种，一种是直接在cmd里输入

```bash
pip install jupyter
```
第二种是通过Anaconda安装，也是我推荐的方式
若没有安装Anaconda，先到[https://www.anaconda.com](https://www.anaconda.com/)下载安装包安装Anaconda，Anaconda完成后，在cmd输入

```bash
conda install jupyter
```
这样，juyter就安装成功了

### 100.jupyter notebook的启动与文件操作
在cmd输入以下命令即可启动jupyter notebook，它将在你的默认浏览器中打开

```bash
jupyter noterbook
```
打开以后界面如下
![](https://img-blog.csdnimg.cn/20200213164611369.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYwODcyMg==,size_16,color_FFFFFF,t_70)
- **jupyter notebook默认的路径是管理员Adminstrator所在文件夹**，默认路径可以修改，在这里不作介绍 
- **jupyter的文件操作可以浏览器界面和文件夹面同时操作**，也就是说你在jupyter文件夹下面新建一个文件，浏览器界面会同时显示。当你需要打开一个`.ipynb`文件，可以将.ipynb直接复制到jupyter的文件夹下面.当然你也可以点击`Upload`来选择你要上传的jupyter notebook的文件
- 点击`Logout`或者关闭cmd和浏览器即可退出jupyter

### 101.jupyter notebook的界面操作和常用快捷键
俗话说得好，磨刀不误砍柴工，熟悉了jupyter的操作和快捷键，使用IPython自然得心应手
点击`New`出现下拉框，在点击Python 3(这里的python 3是Anaconda的python解释器)就可以创建一个`.ipynb`文件
<img src="https://img-blog.csdnimg.cn/20200213170844651.png"   width="30%"><img src="https://img-blog.csdnimg.cn/20200213172110650.png"   width="70%">

- 点击上面`Untitled`可以修改文件名
- 点击`代码`出现下拉框，可以实现`markdown`格式和代码格式的转换
- 点击`Insert`可以选择向前或向后插入代码行
- jupyter notebook有两种模式，一种是`编辑模式`,按`Enter`进入此模式，此时代码行外框呈现出`绿色`，可以对代码行内部进行缩进、删除、运行等操作
另一种是`命令模式`，若进入编辑模式，则按`Esc`进入命令模式，此时代码行外框呈现出`蓝色`
- jupyter常用快捷键
	+ 编辑模式
		* **Shift-Enter**: 运行本单元，选中下一代码行（若下面没有单元，则新建一个单元）
		* **Ctrl-Enter**: 运行本单元
		* **Alt-Enter**: 运行本单元，在下面插入一单元
    + 命令模式
		+ **数字1~6**: 设定1到6级标题
		+ **A**: 在上方插入新单元
		+ **B**: 在下方插入新单元
		+	**连续两下D**: 删除选中的单元
		+ **Shift-K**: 扩大选中上方单元
		+ **Shift-J**: 扩大选中下方单元
		+ **shift-M**：合并单元

	更多快捷键等待你的探索
### 110.IPython 的获取与探索功能
IPython 和 Jupyter 最大的优势之一就是能方便我们搜索函数和文档的功能，帮助我们高效完成工作
+ 使用`?`来获取文档
     我们传统的获取python文档是使用help()
```python
>>>help(list)
Help on class list in module builtins:

class list(object)
 |  list(iterable=(), /)
 |  
 |  Built-in mutable sequence.
 |  
 |  If no argument is given, the constructor creates a new empty list.
 |  The argument must be an iterable if specified.
 |  
 |  Methods defined here:
 |  
 |  __add__(self, value, /)
 |      Return self+value.
    (………………………………………………………………)
```
在IPython中我们可以使用`list？`,显示出的信息更加简明扼要

```python
In[1]:list?
Init signature: list(iterable=(), /)
Docstring:     
Built-in mutable sequence.

If no argument is given, the constructor creates a new empty list.
The argument must be an iterable if specified.
Type:           type
Subclasses:     _HashedSeq, StackSummary, SList, _ImmutableLineList, FormattedText, NodeList, _ExplodedList, Stack, _Accumulator, _ymd, ...
```
`?`也同样适应于`对象的方法`，甚至于对象本身

```python
In [2]: L=[1,2,3]

In [3]: L.append?
Signature: L.append(object, /)
Docstring: Append object to the end of the list.
Type:      builtin_function_or_method

In [4]: L?
Type:        list
String form: [1, 2, 3]
Length:      3
Docstring:
Built-in mutable sequence.

If no argument is given, the constructor creates a new empty list.
The argument must be an iterable if specified.
```
+ 使用`TAB`探索模块
    L后面加上`.`再按`Tab`键即可看到该对象的所有方法
    
```python

In [5]: L.
           append() count    insert   reverse
           clear    extend   pop      sort
           copy     index    remove
```

   也可以输入方法的前面几个字母以缩小搜索范围，若只有一个选项满足搜索条件，则Tab**自动补全**方法

```python
In [6]: L.c
            clear()
            copy()
            count()
```
同样的道理我们也可以应用在导入模块时

```python
In [7]: import ma
                  macpath    man        math
                  mailbox    markupsafe matplotlib
                  mailcap    marshal
```
熟练使用Tab自动补全可以有效提高工作效率

### 111.IPython的魔法命令
IPython的魔法命令显著地将IPython与pyhton区别开来，也彰显了Interactive的内涵
魔法命令分为行魔法(line magic)和单元魔法(cell magic)
+ 行魔法：前缀是一个`%`,只作用于单行
+ 单元魔法：前缀是`%%`，作用于整个单元,方便多行输入
常用的魔法命令有`%paste`、`%cpaste`、`%run`、`%timeit`

这里我只介绍%timeit,其他魔法命令可以使用`%lsmagic`和`?`探索
%timeit，它会自动计算接下来一行的 Python 语句的执行时
间。例如，我们可能想了解生成列表所用的时间：

```python
In [8]: %timeit L = [n ** 2 for n in range(1000)]
375 µs ± 3.07 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```

%timeit 的好处是，它会自动多次执行简短的命令，以获得更稳定的结果。对于多行语句，可以加入第二个 % 符号将其转变成单元魔法，以处理多行输入。例如，下面是 for 循环的同等结构：

```python
In[9]: %%timeit
    ...: L=[]
    ...: for i in range(1000):
    ...:     L.append(i**2)
    ...:
414 µs ± 5.02 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```
可以看出使用range()生成列表比用for循环快一些

-----

>学习IPython网站：
>[http://ipython.org](http://ipython.org)
>[http://github.com/ipython/ipython/wiki/A-gallery-of-interestingIPython-Notebooks/](http://github.com/ipython/ipython/wiki/A-gallery-of-interestingIPython-Notebooks/)
>[http://nbviewer.ipython.org](http://nbviewer.ipython.org/)