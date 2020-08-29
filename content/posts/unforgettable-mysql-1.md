---
author: "ibolee"
date: 2014-09-28
linktitle: mysql-practice-45
tags: ["mysql"]
categories: ["数据"]
title: Myqsl语句经典例题
weight: 10
---
{{< admonition type=tip title="这里是mysql例题导入代码" open=false >}}
```
------------创建数据库---------------
create database data charset=utf8;

------------ 建表语句-----------------
# 学生表 Student：

create table Student(

SId varchar(10) ,

Sname varchar(10),

Sage datetime,

Ssex varchar(10));




# 教师表 Teacher

create table Teacher(

TId varchar(10),

Tname varchar(10)); 



# 科目表 Course

create table Course(

CId varchar(10),

Cname nvarchar(10),

TId varchar(10)); 

# 成绩表 SC

create table SC(

SId varchar(10),

CId varchar(10),

score decimal(18,1)); 


------------ 插入数据语句-----------------

# 学生表 Student：

insert into Student values('01' , '赵雷' , '1990-01-01' , '男');

insert into Student values('02' , '钱电' , '1990-12-21' , '男');

insert into Student values('03' , '孙风' , '1990-05-20' , '男');

insert into Student values('04' , '李云' , '1990-08-06' , '男');

insert into Student values('05' , '周梅' , '1991-12-01' , '女');

insert into Student values('06' , '吴兰' , '1992-03-01' , '女');

insert into Student values('07' , '郑竹' , '1989-07-01' , '女');

insert into Student values('09' , '张三' , '2017-12-20' , '女');

insert into Student values('10' , '李四' , '2017-12-25' , '女');

insert into Student values('11' , '李四' , '2017-12-30' , '女');

insert into Student values('12' , '赵六' , '2017-01-01' , '女');

insert into Student values('13' , '孙七' , '2018-01-01' , '女');



# 科目表 Course

insert into Course values('01' , '语文' , '02'); 

insert into Course values('02' , '数学' , '01'); 

insert into Course values('03' , '英语' , '03'); 



# 教师表 Teacher

insert into Teacher values('01' , '张三');
 
insert into Teacher values('02' , '李四'); 

insert into Teacher values('03' , '王五'); 



# 成绩表 SC

insert into SC values('01' , '01' , 80); 

insert into SC values('01' , '02' , 90); 

insert into SC values('01' , '03' , 99); 

insert into SC values('02' , '01' , 70); 

insert into SC values('02' , '02' , 60); 

insert into SC values('02' , '03' , 80); 

insert into SC values('03' , '01' , 80); 

insert into SC values('03' , '02' , 80); 

insert into SC values('03' , '03' , 80); 

insert into SC values('04' , '01' , 50); 

insert into SC values('04' , '02' , 30); 

insert into SC values('04' , '03' , 20); 

insert into SC values('05' , '01' , 76); 

insert into SC values('05' , '02' , 87); 

insert into SC values('06' , '01' , 31); 

insert into SC values('06' , '03' , 34); 

insert into SC values('07' , '02' , 89); 

insert into SC values('07' , '03' , 98); 

```
{{< /admonition >}}

###例题列表

1:查询课程01比课程02成绩高的学生信息及课程分数

{{< admonition tip "解题代码" false >}}
```
#1.查询01课程比02课程成绩高的学生信息和成绩分数
#学生信息在student这个表中
#成绩分数在sc表中
#目的:01课程比02课程成绩高的学生,01课程和02课程用cid体现,cid只在sc中有
select * from student a
INNER JOIN sc b
on a.SId=b.SId #这里看成第一个大表

INNER JOIN sc c
on b.SId=c.SId and b.CId="01" AND c.cid="02" #这里看成第二个大表
WHERE b.score>c.score #进行分数比较
```
{{< /admonition >}}

2:查询同时存在01课程和02课程的情况
{{< admonition tip "解题代码" false >}}
```
#第一种写法
#查询同时存在01课程和02课程的情况
#01课程和02课程的成绩表都在sc表之中
SELECT *
FROM
(SELECT * FROM sc where cid='01') a
INNER join
(select * from sc where cid='02') b
on a.sid=b.sid
#第二种写法
#这个解决方案相当于,把where条件改加到最下面了
SELECT *
FROM
sc a
INNER join
sc b
on a.sid=b.sid
WHERE a.CId='01' AND b.cid='02'
```
{{< /admonition >}}

3:查询存在01课程但可能不存在02课程的情况(不存在时显示为null)
{{< admonition tip "解题代码" false >}}
```
#第一种写法
#查询存在01课程但可能不存在02课程的情况(不存在时显示为null)
SELECT *
FROM
(select * from sc WHERE cid='01') a
LEFT JOIN (SELECT * FROM sc where CId='02') b
on a.sid=b.sid
#第二种写法
SELECT *
FROM
sc a
LEFT JOIN sc b
on a.sid=b.sid and b.cid='02'
WHERE a.cid='01';
```
{{< /admonition >}}

4:查询不存在01课程,但存在02课程的情况
{{< admonition tip "解题代码" false >}}
```
#第一种写法
SELECT
*
FROM
(SELECT *
FROM sc WHERE sid NOT IN
(SELECT SId FROM sc WHERE CId='01')) A
INNER JOIN SC B
ON A.SID=B.SId AND B.CID='02';
#第二种写法
select *
FROM sc a
WHERE SId not in (SELECT SId from sc where cid='01')#用not in 进行了排除
AND cid='02';git status
```
{{< /admonition >}}
5:查询不存在01课程,但存在02课程的情况
{{< admonition tip "解题代码" false >}}
```
#第一种写法
SELECT
*
FROM
(SELECT *
FROM sc WHERE sid NOT IN
(SELECT SId FROM sc WHERE CId='01')) A
INNER JOIN SC B
ON A.SID=B.SId AND B.CID='02';
#第二种写法
select *
FROM sc a
WHERE SId not in (SELECT SId from sc where cid='01')#用not in 进行了排除
AND cid='02';
```
{{< /admonition >}}
6:查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩
{{< admonition tip "解题代码" false >}}
#解题思路:先查询sid,然后用sid进行匹配;group by配合平均函数使用;
SELECT b.sid,b.Sname,a.avg_score
FROM
(SELECT sid,AVG(score) as avg_score FROM sc GROUP BY SId HAVING avg_score>=60) a
INNER JOIN student b
ON a.sid=b.sid
{{< /admonition >}}
7:查询在 SC(成绩表) 表存在成绩的学生信息;
{{< admonition tip "解题代码" false >}}
#查询在 SC 表存在成绩的学生信息,这题目主要巩固group by的括号内严谨写法,还有b.*可作为查询条件.
select b.*
FROM
(SELECT
SId from
sc GROUP BY sid) a
LEFT JOIN student b
on a.Sid=b.SId;
{{< /admonition >}}