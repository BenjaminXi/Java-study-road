##新建表
```
create table Student(
Sid varchar(10),
Sname varchar(10),
Sage datetime,
Ssex varchar(10)
);
insert into Student values('01' , '赵雷' , '1990-01-01' , '男');
insert into Student values('02' , '钱电' , '1990-12-21' , '男');
insert into Student values('03' , '孙风' , '1990-05-20' , '男');
insert into Student values('04' , '李云' , '1990-08-06' , '男');
insert into Student values('05' , '周梅' , '1991-12-01' , '女');
insert into Student values('06' , '吴兰' , '1992-03-01' , '女');
insert into Student values('07' , '郑竹' , '1989-07-01' , '女');
insert into Student values('08' , '王菊' , '1990-01-20' , '女');
insert into Student values('09' , '孙吴昊' , '1990-01-20' , '女');
insert into Student values('10' , '赵雷' , '1990-01-20' , '女');
create table Course(
Cid varchar(10),
Cname varchar(10),
Tid varchar(10)
);
insert into Course values('01' , '语文' , '02');
insert into Course values('02' , '数学' , '01');
insert into Course values('03' , '英语' , '03');
insert into Course values('04' , '英语' , '01');
create table Teacher(
Tid varchar(10),
Tname varchar(10)
);
insert into Teacher values('01' , N'张三');
insert into Teacher values('02' , N'李四');
insert into Teacher values('03' , N'王五');
insert into Teacher values('04' , N'汪二蛋');
create table SC(
Sid varchar(10),
Cid varchar(10),
score decimal(18,1)
);
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
insert into SC values('08' , '03' , 98);
insert into SC values('09' , '03' , 98);
insert into SC values('10' , '04' , 59);
```
##1 查询”01”课程比”02”课程成绩高的学生的学号；
分析：在sc表中要比较两行的数据大小，一张表是无法比较的，所以用到两张重复的表，考点为表联结和表别名可以不止一次的用到一张表。from语句和where语句这样写from sc as b,sc as c
where b.Sid=c.Sid and b.Cid='01' and c.Cid='02' and b.score>c.score，然后取出Sid,完整的语句如下
方法1：
```
SELECT a.sid
FROM sc a,sc b
WHERE a.sid = b.sid AND a.cid ='01' AND b.cid = '02' AND a.score > b.score;
```
方法2：取出sc表中特定行数据组成新表
```
SELECT a.sid
FROM (SELECT sid,score FROM sc WHERE cid='01') a,(SELECT sid,score FROM sc WHERE cid='02') b
WHERE a.score>b.score AND a.sid=b.sid;
```
##2查询平均成绩大于60分的同学的学号和平均成绩；
考点：group by 分组数据，having 过滤数据，avg聚集函数
```
SELECT sid,AVG(score)
FROM sc
GROUP BY sid HAVING AVG(score)>60;
```
##3查询所有同学的学号、姓名、选课数、总成绩
```
SELECT b.sid,b.sname,COUNT(a.sid) AS number,SUM(a.score) AS total
FROM sc a,student b
WHERE a.sid=b.sid
GROUP BY a.sid
```
方法2：外联结
```
SELECT b.sid,b.sname,COUNT(a.sid) AS number,SUM(a.score) AS total
FROM sc a LEFT OUTER JOIN student b
ON a.sid=b.sid
GROUP BY a.sid
```
##4查询姓“李”的老师的个数；
```
SELECT COUNT(teacher.tid)
FROM teacher 
WHERE teacher.tname LIKE '李%';
```
##5查询没学过“李四”老师课的同学的学号、姓名;
###考点
in操作符，not操作符，子查询
```
SELECT student.sid,student.sname 
FROM student
WHERE sid NOT IN(
SELECT sc.sid
FROM sc,course,teacher
WHERE teacher.tname = '李四' AND teacher.tid=course.tid AND course.cid=sc.cid);
```
##6查询学过“01”课程并且也学过编号“02”课程的同学的学号、姓名；
```
SELECT a.SID,a.SNAME 
FROM 
(SELECT student.SNAME,student.SID FROM student,course,sc WHERE sc.cid='01'AND sc.sid=student.sid AND sc.cid=course.cid) a,
(SELECT student.SNAME,student.SID FROM student,course,sc WHERE sc.cid='02'AND sc.sid=student.sid AND sc.cid=course.cid) b 
WHERE a.sid=b.sid;
```
##7.查询学过“李四”老师所教的所有课的同学的学号、姓名；
```
SELECT sc.sid,student.sname
FROM sc,course,teacher,student
WHERE teacher.tname = '李四' AND teacher.tid=course.tid AND course.cid=sc.cid AND student.sid=sc.sid;
```
##8查询课程编号“02”的成绩比课程编号“01”课程低的所有同学的学号、姓名；




