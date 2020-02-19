---
title: 对python输入流的简单探索
date: 2020-02-14 20：00：00
categories:
	- 语言
	- Python
tags:
	- Python
	- 蓝桥杯
	- 基础操作
excerpt: 用python，你真的会input()了吗？
---

>本文首发于[vito的CSDN博客](https://blog.csdn.net/weixin_43608722/article/details/104306943)，经作者同意后转载。
---

今年的蓝桥杯新增加了python比赛，CCF-CSP认证现在也可以使用python语言，我和身边的一些小伙伴选择了使用pyhton来做算法题。我刚从C/C++转到python有诸多不适，遇到的第一个问题便是python的**输入**问题

我先举一个简单的例子，输入两个整型，用空格隔开,
在C++中非常简单实现

```cpp
int a,b;
cin>>a>>b;
```
C++的输入流`>>`不仅支持按回车分隔输入，也支持按空格分隔输入
刚开始学python的我有了这样先入为主的概念，就写出这样的python的代码

```python
a=input()
b=input()
print(a)
print(b)
```
这样写是没有语法问题的，运行一下输入 1 2，可是当我输入2后按下了回车键，光标提示我还要继续输入，我下意识再按了下回车，输出，本应该出现在两行的1和2竟然出现在了一行

```python
1 2
```

<img src=https://img-blog.csdnimg.cn/2020021409485921.jpg width='50%'>

修改一下程序,去掉print(b)

```python
print(a)
```
在运行程序，输入1 2，点击运行

```python
1 2
```

结果不变，显然1、空格、2都赋值给了a
为什么会出现这样的结果呢，我这里用help查询一下吧

```python
>>> help(input)
Help on built-in function input in module builtins:

input(prompt=None, /)
    Read a string from standard input.  The trailing newline is stripped.
    
    The prompt string, if given, is printed to standard output without a
    trailing newline before reading input.
    
    If the user hits EOF (*nix: Ctrl-D, Windows: Ctrl-Z+Return), raise EOFError.
    On *nix systems, readline is used if available.

```
Read a `string` from standard input.  这句话解释得非常清楚啦，input()是读取了一个字符串。也就是说，刚刚我按下空格时，并没有**结束**当前a=input()这一动作，而是继续读取接下来我从键盘上输入的2，所以b就有接收到2了。
我在Python Shell上再继续验证一下

```python
>>> a=input()
1 2
>>>print("a=",a,"\na's type is",type(a))
a= 1 2
a's type is <class 'str'>
```
python的input()有点像C++的`cin.getline()`，可以接受带空格的字符串，按回车才会结束当前输入。
即使你输入的是整型、浮点型，也会自动转化为字符串

我在[PAT (Basic Level) Practice](https://pintia.cn/problem-sets/994805260223102976/problems/type/7)里找了一个OJ题，来练习一下在OJ遇见此类问题(带空格的输入)应该怎么做
#### <center>[1010 一元多项式求导](https://pintia.cn/problem-sets/994805260223102976/problems/994805313708867584)</center>
>设计函数求一元多项式的导数。（注：x^n  （n为整数）的一阶导数为nx^n−1 。）
>输入格式:
>以指数递降方式输入多项式非零项系数和指数（绝对值均为不超过 1000 的整数）。数字间以`空格`分隔。
>输出格式:
>以与输入相同的格式输出导数多项式非零项的系数和指数。数字间以空格分隔，但结尾**不能有多余空格**。注意“零多项式”的指数和系数都是 0，但是表示为 0 0。
>输入样例:
>3 4 -5 2 6 1 -2 0
>输出样例:
>12 3 -10 1 6 0

ok，读完题感觉很简单一道OJ题，可是对于当时刚学了一个周python满脑子是C++的我来说并不容易，光是输入就让我头疼半天。我仔细回想了一下，问题出在于我对于input()赋给变量一个`字符串`没有清楚的概念

好了，现在我们坚信input()输入的是字符串，接下来就是对字符串的操作了，然而直接对字符进行操作是很生硬的，我首先用`split()`将其转化为`列表`，其中再将其字符转化为整型，剩下对列表操作就行云流水了

```python
st=input()
s=[int(x) for x in st.split()]
result=[]
for i in range(0,len(s),2):
    if s[i+1]!=0:
        result.append(str(int(s[i]*s[i+1])))
        result.append(str(s[i+1]-1))
if len(result)==0:
    print('0 0')
else:
    print(' '.join(result))
```
其实，当你熟练python,前面两句可以简化为以下代码

```python
s=[int(x) for x in input().split()]
```
input()就是一个字符串，大胆地使用.split()就好了

为了强化input()是字符串这一概念呢，我又准备了一道题


  ####      <center>[1009 说反话](https://pintia.cn/problem-sets/994805260223102976/problems/994805314941992960)  </center>
> 给定一句英语，要求你编写程序，将句中所有单词的顺序颠倒输出。
> 输入格式：
> 测试输入包含一个测试用例，在一行内给出总长度不超过 80 的字符串。字符串由若干单词和若干空格组成，其中单词是由英文字母（大小写有区分）组成的字符串，单词之间用 1 个空格分开，输入保证句子末尾没有多余的空格。
> 输出格式：
> 每个测试用例的输出占一行，输出倒序后的句子。
> 输入样例：
> Hello World Here I Come
> 输出样例：
> Come I Here World Hello

经过我的反复修改，最终答案只剩一行代码

```python
print(' '.join(input().split()[::-1]))
```
先用`split()`将input()转化为`字符串列表`,再使用`切片[::-1]`逆序,最后在用' '.join()将字符列表转化为`字符串`输出,这一行代码融合了输入流、输出流、字符串和列表之间的转化，python使用起来确实很流畅
<img src=https://img-blog.csdnimg.cn/20200214103649856.jpg width='50%'>

----
这是Vito的第二篇原创博客，以后我会陆续介绍学习python的一点心得。除了在CSDN上发布博客，我也会在[矿大计算机学院资源传承计划（Resource Inheritance Plan of CUMTCS）](https://github.com/cumtcssuld/RIP_of_CUMTCS)这个GitHub资源库里分享我的学习资料和博客