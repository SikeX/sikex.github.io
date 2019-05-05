---
layout: post
title: "Visualize the world population "
subtitle: "世界人口数据可视化"
date: 2019-04-28 10:26:27
author: "Sike"
header-img:   "img/in-post/1001-header-bg.jpg"
header-mask: 0.3
catalog: true
tag:
  - 可视化
  - python
---

> 可视化老师布置的作业，要求可视化世界人口数据

### 所给数据
给出了六大洲20年的人口数据<br>
![given data](/img/population.jpg)

![data detail](/img/population01.jpg)

### 分析数据

因为要分析的是全世界的数据，而所给数据是六个大洲的数据，而且每个大洲的数据又被分隔成了各个国家的数据。所以数据的整合是必须的。

### 步骤
#### 导入数据
有很多的方法可以读入csv文件，这里选用了pandas库，借助了pandas中read_csv的一些良好特性
```python
pd.read_csv(f,delimiter=",",error_bad_lines=False,skiprows=3)#逗号为分隔符，跳过前三行
data = data.dropna(how='any')#去掉缺失值
```
得到了整齐的数据
![pop2](/img/pop02.jpg)

#### 整合数据
将每个洲所有国家的数据整合到一起
```python
years = data.columns.tolist()
    years.remove(years[0]) #去掉第一个值
    pop = []
    years.reverse() #链表逆序，年份从小到大排列
    for i in years:
        pop.append(data[i].tolist())
    tot = 0
    total = []
    for i in pop:
        for j in i:
            tot += j
        total.append(tot)
```
`total` 里包含的是每个大洲20年的数据

然后分别导入六个大洲的csv即可
```
NA = readcsv('../世界人口数据/人口_北美洲.csv')
EU = readcsv('../世界人口数据/人口_欧洲.csv')
AS = readcsv('../世界人口数据/人口_亚洲.csv')
DY = readcsv('../世界人口数据/人口_大洋洲.csv')
AF = readcsv('../世界人口数据/人口_非洲.csv')
LA = readcsv('../世界人口数据/人口_拉丁美洲.csv')
```
#### 可视化数据
这里使用的是`pyechart`库来进行数据可视化，比较方便

<b>1996-2015全世界总人数条形图<b>
```python
bar.add("人口",
        years,
        pop_total)
bar.render('bar01.html')
```
![bar01](/img/pop_bar01.jpg)
**#1996年和2015年世界人口分布饼图**
```python
page = Page()
x = ['北美洲','欧洲','亚洲','大洋洲','非洲','拉丁美洲']
y1 = [pop['NA'][0], pop['EU'][0] , pop['AS'][0] , pop['DY'][0] , pop['AF'][0] , pop['LA'][0]]
y2 = [pop['NA'][-1], pop['EU'][-1] , pop['AS'][-1] , pop['DY'][-1] , pop['AF'][-1] , pop['LA'][-1]]
pie = Pie("1996年界人口分布")
pie.add("",x, y1,is_label_show = True)
page.add(pie)
pie = Pie("2015年界人口分布")
pie.add("",x, y2,is_label_show = True)
page.add(pie)
page.render('pie01.html')
page
```
![pie](/img/pop_pie.jpg)

还有各种图按照需求添加即可

#### 全部代码
```python
#encoding:utf-8
import pyecharts
import pandas as pd
from pyecharts import Bar
from pyecharts import Line
from pyecharts import Pie
from pyecharts import Page

#读取csv文件，返回包含20年数据的list
def readcsv(path):
    f = open(path)
    data = pd.read_csv(f,delimiter=",",error_bad_lines=False,skiprows=3)#逗号为分隔符，跳过前三行
    data = data.dropna(how='any')#去掉缺失值
    years = data.columns.tolist()
    years.remove(years[0]) #去掉第一个值
    pop = []
    years.reverse() #链表逆序，年份从小到大排列
    for i in years:
        pop.append(data[i].tolist())
    tot = 0
    total = []
    for i in pop:
        for j in i:
            tot += j
        total.append(tot)
    return total

years = ['1996年', '1997年', '1998年', '1999年', '2000年', '2001年', '2002年', '2003年', '2004年', '2005年', '2006年', '2007年', '2008年', '2009年', '2010年', '2011年', '2012年', '2013年', '2014年', '2015年']
pop = {}
NA = readcsv('../世界人口数据/人口_北美洲.csv')
EU = readcsv('../世界人口数据/人口_欧洲.csv')
AS = readcsv('../世界人口数据/人口_亚洲.csv')
DY = readcsv('../世界人口数据/人口_大洋洲.csv')
AF = readcsv('../世界人口数据/人口_非洲.csv')
LA = readcsv('../世界人口数据/人口_拉丁美洲.csv')

#将各个洲的数据存放在字典里
pop = {'NA':NA,'EU':EU,'AS':AS,'DY':DY,'AF':AF,'LA':LA}
#1996-2015全世界总人数
pop_total = []
for i in range(0, 20):
    #print(pop['NA'][i] + pop['EU'][i] + pop['AS'][i] + pop['DY'][i] + pop['AF'][i] + pop['LA'][i])
    #pop_total[i] = pop['NA'][i] + pop['EU'][i] + pop['AS'][i] + pop['DY'][i] + pop['AF'][i] + pop['LA'][i]
    pop_total.append(pop['NA'][i] + pop['EU'][i] + pop['AS'][i] + pop['DY'][i] + pop['AF'][i] + pop['LA'][i])

#1996-2015全世界总人数条形图
bar = Bar("20年世界人口总数")
bar.add("人口",
        years,
        pop_total)
bar.render('bar01.html')

#各个洲人口条形图
print()
bar = Bar("各个洲人口",width=1400,height=700)
bar.add("欧洲",years,pop['EU'])
bar.add("亚洲",years,pop['AS'])
bar.add("拉丁",years,pop['LA'])
bar.add("北美洲",years,pop['NA'])
bar.add("大洋洲",years,pop['DY'])
bar.add("非洲",years,pop['AF'])
bar.render('bar02.html')
bar

#1996-2015各个洲总人数折线图
line = Line("各个洲人口",width=1400,height=700)
line.add("欧洲",years,pop['EU'])
line.add("亚洲",years,pop['AS'])
line.add("拉丁",years,pop['LA'])
line.add("北美洲",years,pop['NA'])
line.add("大洋洲",years,pop['DY'])
line.add("非洲",years,pop['AF'])
line.render('line01.html')
line

#1996年和2015年世界人口分布饼图
page = Page()
x = ['北美洲','欧洲','亚洲','大洋洲','非洲','拉丁美洲']
y1 = [pop['NA'][0], pop['EU'][0] , pop['AS'][0] , pop['DY'][0] , pop['AF'][0] , pop['LA'][0]]
y2 = [pop['NA'][-1], pop['EU'][-1] , pop['AS'][-1] , pop['DY'][-1] , pop['AF'][-1] , pop['LA'][-1]]
pie = Pie("1996年界人口分布")
pie.add("",x, y1,is_label_show = True)
page.add(pie)
pie = Pie("2015年界人口分布")
pie.add("",x, y2,is_label_show = True)
page.add(pie)
page.render('pie01.html')
page
```
