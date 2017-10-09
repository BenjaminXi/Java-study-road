## 新建表
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
## 1 查询”01”课程比”02”课程成绩高的学生的学号；
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
## 2查询平均成绩大于60分的同学的学号和平均成绩；
考点：group by 分组数据，having 过滤数据，avg聚集函数
```
SELECT sid,AVG(score)
FROM sc
GROUP BY sid HAVING AVG(score)>60;
```
## 3查询所有同学的学号、姓名、选课数、总成绩
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
## 4查询姓“李”的老师的个数；
```
SELECT COUNT(teacher.tid)
FROM teacher 
WHERE teacher.tname LIKE '李%';
```
## 5查询没学过“李四”老师课的同学的学号、姓名;
考点：in操作符，not操作符，子查询
```
SELECT student.sid,student.sname 
FROM student
WHERE sid NOT IN(
SELECT sc.sid
FROM sc,course,teacher
WHERE teacher.tname = '李四' AND teacher.tid=course.tid AND course.cid=sc.cid);
```
## 6查询学过“01”课程并且也学过编号“02”课程的同学的学号、姓名；
```
SELECT a.SID,a.SNAME 
FROM 
(SELECT student.SNAME,student.SID FROM student,course,sc WHERE sc.cid='01'AND sc.sid=student.sid AND sc.cid=course.cid) a,
(SELECT student.SNAME,student.SID FROM student,course,sc WHERE sc.cid='02'AND sc.sid=student.sid AND sc.cid=course.cid) b 
WHERE a.sid=b.sid;
```
## 7.查询学过“李四”老师所教的所有课的同学的学号、姓名；
```
SELECT sc.sid,student.sname
FROM sc,course,teacher,student
WHERE teacher.tname = '李四' AND teacher.tid=course.tid AND course.cid=sc.cid AND student.sid=sc.sid;
```
## 8查询课程编号“02”的成绩比课程编号“01”课程低的所有同学的学号、姓名；
```
SELECT a.sid,student.sname
FROM sc a,sc b,student
WHERE a.sid = b.sid AND a.sid=student.sid AND a.cid ='01' AND b.cid = '02' AND a.score > b.score;
```
这道题和1题很类似，不同的是需要输出姓名，所以联结一个student表即可。
## 9查询所有课程成绩小于 60 分的同学的学号、姓名；
```
SELECT sid,sname 
FROM student 
WHERE sid NOT IN(
	SELECT sc.sid
	FROM sc,student
	WHERE sc.sid=student.sid AND score>60);
```
## 10查询没有学全所有课的同学的学号、姓名；
```
SELECT Student.sid,Student.Sname  
FROM Student,SC  
WHERE Student.sid=SC.sid 
GROUP BY Student.sid,Student.Sname
HAVING COUNT(cid) <(SELECT COUNT(cid) FROM Course); 
```
## 11查询至少有一门课与学号为“01”的同学所学相同的同学的学号和姓名；
```
SELECT DISTINCT s.sid, s.sname
FROM student s,sc c
WHERE s.sid = c.sid AND c.cid IN (SELECT cid FROM sc WHERE sid='01');
```
## 12查询至少学过学号为“01”同学所有一门课的其他同学学号和姓名； 
```
SELECT DISTINCT s.sid, s.sname
FROM student s,sc c
WHERE s.sid = c.sid AND c.cid IN (SELECT cid FROM sc WHERE sid='01');
```
## 13把“SC”表中“李四”老师教的课的成绩都更改为此课程的平均成绩；
```
UPDATE sc
SET sc.score = (
	SELECT AVG(sc.score)
	FROM teacher,course,sc
	WHERE tname='李四' AND teacher.tid=course.tid AND course.cid=sc.cid);
```
## 14查询和“02”号的同学学习的课程完全相同的其他同学学号和姓名；
```
SELECT sid 
FROM sc
WHERE cid IN (
	SELECT cid
	FROM sc
	WHERE sid='02')
GROUP BY sid
HAVING COUNT(*) = (
	SELECT COUNT(*) 
	FROM SC 
	WHERE Sid='02');
```
## 15删除学习“李四”老师课的 SC 表记录；
```
DELETE FROM sc
WHERE sc.cid IN(
SELECT course.cid
FROM teacher,course
WHERE tname='李四' AND teacher.tid=course.tid );
```
## 16向 SC 表中插入一些记录，这些记录要求符合以下条件：没有上过编号“02”课程的同学学号、02课的平均成绩； 
```
INSERT INTO sc
SELECT Sid,'02',(SELECT AVG(score) FROM SC WHERE Cid='02')
FROM Student WHERE Sid NOT IN (SELECT Sid FROM SC WHERE Cid='02'); 
```
该条语句未通过测试，待更改。
## 17按平均成绩从高到低显示所有学生的“语文”、“数学”、“英语”三门的课程成绩，按如下形式显示： 学生 ID,语文,数学,英语,有效课程数,有效平均分;
```
SELECT Sid AS 学生ID ,(SELECT score FROM SC WHERE SC.Sid=t.Sid AND Cid='01') AS 语文 
                    ,(SELECT score FROM SC WHERE SC.Sid=t.Sid AND Cid='02') AS 数学 
                    ,(SELECT score FROM SC WHERE SC.Sid=t.Sid AND Cid='03') AS 英语 
                    ,COUNT(*) AS 有效课程数, AVG(t.score) AS 平均成绩 
    FROM SC AS t
    GROUP BY Sid
    ORDER BY AVG(t.score) DESC; 
```
## 18.查询各科成绩最高和最低的分：以如下形式显示：课程ID，最高分，最低分；
```
SELECT cid AS 课程ID,MAX(score) AS 最高分,MIN(score) AS 最低分
FROM sc
GROUP BY cid;
```
## 19.按各科平均成绩从低到高和及格率的百分数从高到低顺序
```
SELECT cid AS 课程ID,AVG(score) AS 平均分
FROM sc
GROUP BY cid
ORDER BY AVG(score);
```
没有实现及格率的百分数排序
## 20.查询如下课程平均成绩和及格率的百分数(用"1 行"显示): 语文（01），数学（02），英语（03）；
待解答
## 21.查询不同老师所教不同课程平均分从高到低显示
```
SELECT t.tid AS 教师ID,t.tname AS 教师姓名,c.cid AS 课程ID,c.cname AS 课程名称,AVG(score) AS 平均成绩 
FROM sc,Course AS c,Teacher AS t
WHERE sc.cid=c.cid AND c.tid=t.tid 
GROUP BY c.cid 
ORDER BY AVG(score) DESC
```
## 22.查询如下课程成绩第 3 名到第 6 名的学生成绩单：语文（01），数学（02），英语（03）
[学生 ID],[学生姓名],语文,数学,英语,平均成绩

## 23.统计列印各科成绩,各分数段人数:课程 ID,课程名称,[100-85],[85-70],[70-60],[< 60]
```
SELECT SC.Cid AS 课程ID, Cname AS 课程名称 
    ,SUM(CASE WHEN score BETWEEN 85 AND 100 THEN 1 ELSE 0 END) AS "[100 - 85]" 
    ,SUM(CASE WHEN score BETWEEN 70 AND 85 THEN 1 ELSE 0 END) AS "[85 - 70]" 
    ,SUM(CASE WHEN score BETWEEN 60 AND 70 THEN 1 ELSE 0 END) AS "[70 - 60]" 
    ,SUM(CASE WHEN score < 60 THEN 1 ELSE 0 END) AS "[<60]" 
FROM SC,Course 
WHERE SC.Cid=Course.Cid 
GROUP BY SC.Cid,Cname;
```
考点：case语句
## 24.查询学生平均成绩及其名次 
```
SELECT 1+(
	SELECT COUNT(*) 
	FROM (SELECT sid,AVG(score) AS 平均成绩 FROM sc GROUP BY sid) AS T1 
	WHERE T1.平均成绩>T2.平均成绩
	)AS RANK,sid,平均成绩
FROM (SELECT sid,AVG(score) AS 平均成绩 FROM sc GROUP BY sid)
AS T2 ORDER BY 平均成绩 DESC;
```
## 25.查询各科成绩前三名的记录:(不考虑成绩并列情况) 
```
 SELECT cid,sname,score 
 FROM student s,sc
 WHERE s.sid=sc.sid AND cid ='01'
 ORDER BY score DESC LIMIT 3
```
 只有01课程的前三名，显示所有科目的前三名待解决。
## 26.查询每门课程被选修的学生数
```
SELECT cid,COUNT(*)
FROM sc
GROUP BY cid;
```
## 27.查询出只选修了一门课程的全部学生的学号和姓名
```
SELECT sc.sid,student.sname
FROM sc,student
WHERE sc.sid=student.sid
GROUP BY student.sid
HAVING COUNT(*)=1
```
## 28.查询男生、女生人数
```
SELECT ssex,COUNT(*)
FROM student
GROUP BY ssex
```
## 29、查询姓“张”的学生名单
```
SELECT COUNT(*)
FROM student
WHERE sname LIKE '张%';
```
## 30、查询同名同性学生名单，并统计同名人数
```
SELECT sname,COUNT(*)
FROM student
GROUP BY sname
HAVING COUNT(sname)>1;
```
## 31、1991 年出生的学生名单(注：Student 表中 Sage 列的类型是 datetime)
```
SELECT sname,sage
FROM student
WHERE YEAR(sage)=1991;
```
## 32.查询每门课程的平均成绩，结果按平均成绩升序排列，平均成绩相同时，按课程号降序排列
```
SELECT cid,AVG(score)
FROM sc
GROUP BY cid
ORDER BY AVG(score),cid DESC;
```
## 33.查询平均成绩大于 85 的所有学生的学号、姓名和平均成绩
```
SELECT sc.sid,sname,AVG(score)
FROM sc,student
WHERE sc.sid=student.sid
GROUP BY sc.sid
HAVING AVG(score)>85;
```
## 34.查询课程名称为“语文”，且分数低于 60 的学生姓名和分数
```
SELECT sc.sid,student.sname,sc.score
FROM sc,course,student
WHERE course.cname='语文' AND course.cid=sc.cid AND sc.sid=student.sid AND sc.score<60;
```
## 35.查询所有学生的选课情况；
```
SELECT SC.Sid,SC.Cid,Sname,Cname 
FROM SC,Student,Course 
WHERE SC.Sid=Student.Sid AND SC.Cid=Course.Cid ORDER BY sc.sid; 
```
## 36.查询任何一门课程成绩在70分以上的姓名、课程名称和分数；
```
```
## 37.查询不及格的课程，并按课程号从大到小排列 
SELECT cid,sid FROM sc WHERE score < 60 ORDER BY cid 

## 38.查询课程编号为且课程成绩在分以上的学生的学号和姓名；
select student.sid,student.sname from sc,student where sc.cid=1 and sc.score>60 and sc.sid=student.sid

## 39.求选了课程的学生人数 

## 40.查询选修“叶平”老师所授课程的学生中，成绩最高的学生姓名及其成绩
select student.sname,sc.score from sc,student,teacher,course c where teacher.tname='李子'
and teacher.tid=c.tid and c.cid=sc.cid and sc.sid=student.sid and sc.score=(select max(score)from sc where sc.cid=c.cid)

## 41.查询各个课程及相应的选修人数
select sc.cid ,count(sc.sid)from sc,student where sc.sid=student.sid group by sc.cid 

## 42.查询不同课程成绩相同的学生的学号、课程号、学生成绩

## 43.查询每门功成绩最好的前两名

## 44.统计每门课程的学生选修人数（超过人的课程才统计）。要求输出课程号和选修人数，查询结果按人数降序排列，查询结果按人数降序排列，若人数相同，按课程号升序排列
select sc.cid,count(sc.cid)from sc,course where sc.cid=course.cid group by sc.cid  order by sc.cid desc

## 45.检索至少选修两门课程的学生学号
SELECT sid FROM  sc group  by  sid having  count(*)  >  =  2  

rownum的用法
查询所有成绩第二名到第四名的成绩
select * from （select rownum p,t.score from（SELECT s.score score FROM sc s ORDER BY score desc）t ）tt where tt.p>1 and tt.p<5

## 46.查询全部学生都选修的课程的课程号和课程名 

## 47.查询没学过“叶平”老师讲授的任一门课程的学生姓名
select distinct sid from sc where sid not in(select sc.sid from sc,course,teacher where sc.cid=course.cid and course.tid=teacher.tid and 
teacher.tname='杨巍巍')

## 48.查询两门以上不及格课程的同学的学号及其平均成绩

## 49.检索“”课程分数小于，按分数降序排列的同学学号
select sc.sid from sc,course where sc.cid=course.cid and course.cname='java' and sc.score<90

## 50.删除“”同学的“”课程的成绩
delete from sc where sid=1 and cid=1
