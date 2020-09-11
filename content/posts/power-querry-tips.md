---
title: "Power Querry操作小技巧"
date: 2020-02-11T09:19:36+08:00
linktitle: Power-Querry-Tips
tags: ["PowerBi","powerbi tips"]
categories: ["数据"]
---
1. 设置中打开power query编辑栏;

解决方法:

![打开命令编辑栏](https://img.ibolee.com/git_blog/pqtips0.png)

![在选项卡设置中设置](https://img.ibolee.com/git_blog/pqtips1.png)

2. power query不要自动添加"更改数据类型"
如果添加了自动更改数据类型,在pq原表中如果删了数据列,pq会报错:expresssion:error找不到表的""列;

解决方法:

设置----选项和设置----选项----类型加载----自动检测未结构化源的列类型和标题(去掉对勾)
![](https://img.ibolee.com/git_blog/pqtips3.png)
数据清洗的过程结束后,最好统一修改一下所有列的数据类型,上述方法只是临时解决方法;
3. power qyery报错以后的处理步骤;
发现报错的时候,先把步骤栏的步骤选到最后一步骤,然后再点转到错误;
步骤操作记录里会跳转到出问题的步骤,修改对应命令框内的内容;
![](https://img.ibolee.com/git_blog/pqtips4.png)

PQ出错的三种常见原因:

+ 删除列、修改列、数据类型改变、改名变位导致的;
+ 修改、插入、删除步骤，导致前后不一致，进而出错;
+ PQ里面的功能，都是通过M函数实现的，有很小概率M语言会更新，旧的写法就会报错；
4. 降低power query报错的几个方法:

+ 删除掉系统自动添加的“更改的类型”;
+ 不要使用删除列,使用删除其他列;选中要保留的列,点击删除其他列;
+ 避免调整列的顺序,顺序列调整后的容错率较低;
  如果发现报错的话,会导致俩个
5. 修改power query数据路径引用和power query引用的表选项卡更名错误;
+ pq数据路径引用出错,重新修改一下数据源,修改后倒序点选一下操作步骤进行更新,修改后依然有报错可以看一下关联的其它表的引用路径是否改变;
+ pq引用Sheet重命名需要修改一下选项卡名称,点转到错误即有提示,修改后倒序点选一下操作步骤即可.
6. 当表的路径需要移动时,批量修改power query中引用表的路径;
引用表的时候,引用一个空白表;取名:0文件路径.xlsx,
在这个表的a1单元格中输入:
```
=TRIM(LEFT(SUBSTITUTE(CELL(filename), [,REPT(,999))999)
```
导入到pq里面,右键-深化,然后再pq设置-选项卡中,把隐私级别改成忽略,隐私级别低;
![](https://img.ibolee.com/git_blog/pqtips5.png) ,修改数据源中引用的数据路径,最后,保存即可.
a721-章5-class20
7. power query的数据管理中,俩个复制代表什么含义?
第一个复制只是复制,第一个复制可以把pq中的公式粘贴到excel中去;
第二个复制是把整个查询进行一个复制,包括数据和操作步骤;
![](https://img.ibolee.com/git_blog/pqtips6.png)
8. power pivot和power query都可以做的分类操作,在哪里做比较好?
比如:Power Pivot中使用 Summarize来建表,Power Query中使用分组依据来建表的区别是:pq可以进行列排序,而且运算速度更快.
9. power query中添加列为1位数的编号补0操作;

![](https://img.ibolee.com/git_blog/pqtips7.png)

添加列时,原表的数据类型是文本,则可以用上图公式自动补齐;

10. power query导入网页数据后的必要操作;
遇到特别复杂的网页页面,点击使用web表推理进行数据导入;
如果还是遇到导入的数据空白的话,在导入数据的时候操作:
![](https://img.ibolee.com/git_blog/pq%E5%AF%BC%E5%85%A5%E7%BD%91%E9%A1%B5%E6%95%B0%E6%8D%AE.png)
然后:
![](https://img.ibolee.com/git_blog/pq%E5%AF%BC%E5%85%A5%E7%BD%91%E9%A1%B5%E6%95%B0%E6%8D%AE2.png)
导入网页数据后的必要操作就是:
+ 转换-格式-清除(删除非打印字符)
+ 转换-替换空格
  
11.用函数批量获取天气数据
![](https://img.ibolee.com/git_blog/%E5%87%BD%E6%95%B0%E8%8E%B7%E5%8F%96%E5%A4%A9%E6%B0%94%E6%95%B0%E6%8D%AE.png)
