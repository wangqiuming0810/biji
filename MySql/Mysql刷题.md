# mysql 查询笔记 & 刷题

推荐博客：[狂神](https://mp.weixin.qq.com/s?__biz=Mzg2NTAzMTExNg==&mid=2247484207&idx=1&sn=2ba333652e06e6b2dcfa949de09aea70&chksm=ce61058cf9168c9aa847f2b3ad54476596816d2a6a04a9481aa6bc28f435b09fb422ac2262e0&mpshare=1&scene=23&srcid=1027EJLUpGmrxt0Qe1P545S7&sharer_sharetime=1635348991668&sharer_shareid=787e9cb76053885b54b02eae7ca9865e#rd)



### 基本查询

```mysql
select * from 表的名字 
```



### 挑选第几条语句到第几条语句

```mysql
SELECT device_id from user_profile LIMIT 0,2
```



###  修改列名

```mysql
SELECT device_id 'user_infors_example' from user_profile LIMIT 0,2
```



### 带查询条件的查询

```mysql
SELECT device_id ,university from user_profile where university='北京大学'

-- 题目：现在运营想要针对24岁以上的用户开展分析，请你取出满足条件的用户明细数据。
SELECT device_id ,gender,age,university from user_profile where age>24

-- 现在运营想要针对20岁及以上且23岁及以下的用户开展分析，请你取出满足条件的用户明细数据。
SELECT device_id ,gender,age from user_profile where age>=20 and age<=23

-- 题目：现在运营想要查看除复旦大学以外的所有用户明细，请你取出相应数据
SELECT device_id,gender,age,university from user_profile where university !='复旦大学'

-- 请你取出所有年龄值不为空的用户明细数据。
SELECT device_id,gender,age,university from user_profile where age is not NULL


```



### 排序

```mysql
order by 字段名  ASC[升序] DESC[降序]
```

不写条件的默认是 升序排列

```mysql
-- 现在运营想要取出用户信息表中的用户年龄，请取出相应数据，并按照年龄升序排序。
SELECT device_id,age from user_profile ORDER BY age ASC
-- 多个字段排序 order by 字段名1+排序规则，字段名2+排序规则
SELECT device_id,gpa,age from user_profile order by gpa asc,age asc;

```



### 聚集函数 SUM，COUNT， MAX，MIN

对哪个count 计数就对哪个分组



练习：

```mysql
 -现在运营想要了解2021年8月份所有练习过题目的总用户数和练习过题目的总次数，请取出相应结果
select
    count(distinct device_id) as did_cnt,
    count(question_id) as question_cnt
from question_practice_detail
where date like "2021-08%"
```

### 逻辑运算符

and  ,or   **and的优先级要大于 or 所以要打上括号**

```mysql 
-- 现在运营想要找到男性且GPA在3.5以上的用户进行调研，请你取出相关数据。
SELECT device_id,gender,age,university,gpa from user_profile where gender='male' and gpa>3.5

select device_id,gender,age,university,gpa from user_profile
where (university='山东大学' and gpa>3.5 )
or (university="复旦大学" and gpa>3.8);
```



### in    NOT  IN

```mysql
select device_id,gender,age,university,gpa from user_profile
where university in('北京大学','复旦大学','山东大学');
```



### 字符匹配

一般形式为：

列名 [NOT ] LIKE

匹配串中可包含如下四种通配符：
_：匹配任意一个字符；
%：匹配0个或多个字符；
[ ]：匹配[ ]中的任意一个字符(若要比较的字符是连续的，则可以用连字符“-”表 达 )；
[ ^  ]：不匹配[ ]中的任意一个字符。

例23．查询学生表中姓‘张’的学生的详细信息。

```mysql
SELECT` `* ``FROM` `学生表 ``WHERE` `姓名 ``LIKE` `‘张%’
```

例24．查询姓“张”且名字是3个字的学生姓名。

```mysql
SELECT` `* ``FROM` `学生表 ``WHERE` `姓名 ``LIKE` `'张__’
```

如果把姓名列的类型改为nchar(20)，在SQL Server 2012中执行没有结果。原因是姓名列的类型是char(20)，当姓名少于20个汉字时，系统在存储这些数据时自动在后边补空格，空格作为一个字符，也参加LIKE的比较。可以用rtrim()去掉右空格。

```mysql
SELECT * FROM 学生表 WHERE rtrim(姓名) LIKE '张__'
```

例25.查询学生表中姓‘张’、姓‘李’和姓‘刘’的学生的情况。

```mysql
SELECT * FROM 学生表 WHERE 姓名 LIKE '[张李刘]%'
```

例26.查询学生表表中名字的第2个字为“小”或“大”的学生的姓名和学号。

```mysql
SELECT` `姓名,学号 ``FROM` `学生表 ``WHERE` `姓名 ``LIKE` `'_[小大]%'
```

例27.查询学生表中所有不姓“刘”的学生。

```mysql
SELECT` `姓名 ``FROM` `学生 ``WHERE` `姓名 ``NOT` `LIKE` `'刘%’
```

例28.从学生表表中查询学号的最后一位不是2、3、5的学生信息。

```mysql
SELECT` `* ``FROM` `学生表 ``WHERE` `学号 ``LIKE` `'%[^235]'
```

### round函数

在mysql中，round函数用于数据的四舍五入，它有两种形式：

1、round(x,d)  ，x指要处理的数，d是指保留几位小数

这里有个值得注意的地方是，d可以是负数，这时是指定小数点左边的d位整数位为0,同时小数位均为0；

2、round(x)  ,其实就是round(x,0),也就是默认d为0；

```mysql
select 
  count(gender) as male_num,
  round(avg(gpa), 1) as avg_gpa
from user_profile where gender="male";
```



### having

一般用来限制聚集函数之后的 条件

```mysql
select
    university,
    avg(question_cnt) as avg_question_cnt,
    avg(answer_cnt) as avg_answer_cnt
from user_profile
group by university
having avg_question_cnt<5 or avg_answer_cnt<20
```



### 连接查询

```mysql
/*
连接查询
   如需要多张数据表的数据进行查询,则可通过连接运算符实现多个查询
内连接 inner join
   查询两个表中的结果集中的交集
外连接 outer join
   左外连接 left join
       (以左表作为基准,右边表来一一匹配,匹配不上的,返回左表的记录,右表以NULL填充)
   右外连接 right join
       (以右表作为基准,左边表来一一匹配,匹配不上的,返回右表的记录,左表以NULL填充)
       
等值连接和非等值连接

自连接
*/

-- 查询参加了考试的同学信息(学号,学生姓名,科目编号,分数)
SELECT * FROM student;
SELECT * FROM result;

/*思路:
(1):分析需求,确定查询的列来源于两个类,student result,连接查询
(2):确定使用哪种连接查询?(内连接)
*/
SELECT s.studentno,studentname,subjectno,StudentResult
FROM student s
INNER JOIN result r
ON r.studentno = s.studentno

-- 右连接(也可实现)
SELECT s.studentno,studentname,subjectno,StudentResult
FROM student s
RIGHT JOIN result r
ON r.studentno = s.studentno

-- 等值连接
SELECT s.studentno,studentname,subjectno,StudentResult
FROM student s , result r
WHERE r.studentno = s.studentno

-- 左连接 (查询了所有同学,不考试的也会查出来)
SELECT s.studentno,studentname,subjectno,StudentResult
FROM student s
LEFT JOIN result r
ON r.studentno = s.studentno

-- 查一下缺考的同学(左连接应用场景)
SELECT s.studentno,studentname,subjectno,StudentResult
FROM student s
LEFT JOIN result r
ON r.studentno = s.studentno
WHERE StudentResult IS NULL

-- 思考题:查询参加了考试的同学信息(学号,学生姓名,科目名,分数)
SELECT s.studentno,studentname,subjectname,StudentResult
FROM student s
INNER JOIN result r
ON r.studentno = s.studentno
INNER JOIN `subject` sub
ON sub.subjectno = r.subjectno
```

