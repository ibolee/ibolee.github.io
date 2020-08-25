# Myqsl语句经典例题

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
SELECT *
FROM
student a
INNER JOIN sc b
on a.SId=b.SId
inner join sc c
on a.sid=c.SId AND b.cid=01 AND c.CId=02
WHERE b.score>c.score
```
{{< /admonition >}}

2:查询同时存在01课程和02课程的情况
{{< admonition tip "解题代码" false >}}
```
#第一种写法
SELECT *
FROM
sc a
INNER JOIN sc b
on a.SId=b.SId AND a.cid="01" and b.CId="02"
#第二种写法
SELECT *
FROM (SELECT * FROM sc WHERE CId='01' ) a
INNER JOIN (SELECT * FROM sc WHERE CId='02' ) b
ON a.SId=b.SId;
```
{{< /admonition >}}

3:查询存在01课程但可能不存在02课程的情况(不存在时显示为null)
{{< admonition tip "解题代码" false >}}
```
SELECT *
FROM (SELECT * FROM sc WHERE CId='01' ) a
LEFT JOIN sc b
ON a.SId=b.SId AND b.CId='02'
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
