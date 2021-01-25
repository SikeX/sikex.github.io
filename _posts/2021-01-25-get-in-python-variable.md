---
layout:       post
title:        "python学习之基本数据类型"
subtitle:     "Get in python basic data type"
date:         2021-01-25 19:45:00
author:       "Sike"
header-img:   "img/in-post/1001-header-bg.jpg"
header-mask:  0.3
catalog: true
tags:
    - Python
---

# python学习之基本数据类型

---

Python万物皆对象(object)，可以通过type查看其类型，是对象则必有属性（attributes）和方法（methods）。

### 整形
```python
#整形
a = 123
#type() 查看对象类型
print(a,type(a))
#dir(a),help(a) 查看对象的属性和方法
dir(a)
# with the -- is methor, without the -- is the attribute
a.bit_length()
```
    123 <class 'int'>
    7

### 浮点型
```python
#浮点型
b = 123.0
print(b,type(b))
```

    123.0 <class 'float'>


### bool型
```python
# bool型
t = True
print(t,type(t))
```

    True <class 'bool'>


上节介绍的整型、浮点型和布尔型都可以看成是单独数据，而这些数据都可以放在一个容器里得到一个「容器类型」的数据，比如：



* 字符 (str) 是一容器的字节 char，注意 Python 里面没有 char 类型的数据，可以把单字符的 str 当做 char。



* 元组 (tuple)、列表 (list)、字典 (dict) 和集合 (set) 是一容器的任何类型变量。


```python
s1 = 'I love python!'
print(s1, type(s1))
#look up the comman methors for str
#dir(str)
s1.split()
```

    I love python! <class 'str'>
    ['I', 'love', 'python!']



### 索引和切片
```python
#索引和切片
s = 'Python'
print( s )
print( s[2:4] ) #包头不包尾
print( s[-5:-2] ) #负索引从右往左
print( s[2:] ) #第三个元素到末尾
print( s[-1] ) #最后一个元素
```

    Python
    th
    yth
    thon
    n


### 元组
元组」定义语法为 


(元素1, 元素2, ..., 元素n)


关键点是「小括号 ()」和「逗号 ,」


* 小括号把所有元素绑在一起

* 逗号将每个元素一一分开


```python
t1 = (1, 10.21, "python")
print(t1, type(t1))
```

    (1, 10.21, 'python') <class 'tuple'>


元组有不可更改 (immutable) 的性质，因此不能直接给元组的元素赋值,但是元组中若是有可更改的对象（例如list）,该对象是可以修改的


```python
t2 = (1,[1,2,'python'],10.21)
t2[1].append('c++')
t2
```




    (1, [1, 2, 'python', 'c++'], 10.21)



元组拼接 (concatenate) 有两种方式，用「加号 +」和「乘号 *」，前者首尾拼接，后者复制拼接。


```python
(1, 10.31, 'python') + ('data', 11) + ('OK',)
(1, 10.31, 'python') * 2
```




    (1, 10.31, 'python', 1, 10.31, 'python')



### 列表
「列表」定义语法为 



[元素1, 元素2, ..., 元素n]



关键点是「中括号 []」和「逗号 ,」



* 中括号把所有元素绑在一起

* 逗号将每个元素一一分开




```python
l = [1, 10.31,'python']
print(l, type(l))
```

    [1, 10.31, 'python'] <class 'list'>



```python
#附加
l.append(['hello','hi'])
print(l)
l.extend(['you','are','welcome'])
print(l)
```

    [1, 10.31, 'python', ['hello', 'hi']]
    [1, 10.31, 'python', ['hello', 'hi'], 'you', 'are', 'welcome']



```python
#插入
l.insert(1,'insert')
print(l)
```

    [1, 'insert', 10.31, 'python', ['hello', 'hi'], 'you', 'are', 'welcome']



```python
#删除
l.remove('python')
l
```




    [1, 'insert', 10.31, ['hello', 'hi'], 'you', 'are', 'welcome']




```python
#删除并返回
p = l.pop(1)
print(p)
print(l)
```

    insert
    [1, 10.31, ['hello', 'hi'], 'you', 'are', 'welcome']


### 切片
切片的通用写法是

> start : stop : step

step默认为1

## 字典
「字典」定义语法为 



{元素1, 元素2, ..., 元素n}



其中每一个元素是一个「键值对」- 键:值 (key:value)



关键点是「大括号 {}」,「逗号 ,」和「分号 :」



* 大括号把所有元素绑在一起

* 逗号将每个键值对一一分开

* 分号将键和值分开


```python
d = {
'Name' : 'Tencent',
'Country' : 'China',
'Industry' : 'Technology',
'Code': '00700.HK',
'Price' : '361 HKD'
}
print( d, type(d) )
```

    {'Name': 'Tencent', 'Country': 'China', 'Industry': 'Technology', 'Code': '00700.HK', 'Price': '361 HKD'} <class 'dict'>


字典里的键是不可更改的，因此只有那些不可更改的数据类型才能当键，比如整数 (虽然怪怪的)、浮点数 (虽然怪怪的)、布尔 (虽然怪怪的)、字符、元组 (虽然怪怪的)，而列表却不行，因为它可更改。

## 集合
「集合」有两种定义语法，第一种是



{元素1, 元素2, ..., 元素n}



关键点是「大括号 {}」和「逗号 ,」



* 大括号把所有元素绑在一起

* 逗号将每个元素一一分开



第二种是用 set() 函数，把列表或元组转换成集合。


set( 列表 或 元组 )


```python
A = set(['u', 'd', 'ud', 'du', 'd', 'du'])
B = {'d', 'dd', 'uu', 'u'}
print( A )
print( B )
```

    {'d', 'u', 'du', 'ud'}
    {'d', 'uu', 'u', 'dd'}


从 A 的结果发现集合的两个特点：无序 (unordered) 和唯一 (unique)。


## 参考文章
[公众号-王的机器-盘一盘 Python 系列 1 - 入门篇 (上)](https://mp.weixin.qq.com/s/c5NEDrTMOm8MjuM67HJ1aQ)