# [MySQL开发中常用的查询语句总结](https://www.cnblogs.com/royfans/p/10097175.html)

### 1、查询数值型数据:

```mysql
SELECT * FROM tb_name WHERE sum > 100;

查询谓词:>,=,<,<>,!=,!>,!<,=>,=<
```

 

### 2、查询字符串

```mysql
SELECT * FROM tb_stu WHERE sname = ‘Cricode.com’

SELECT * FROM tb_stu WHERE sname like ‘Uncle%Too’

SELECT * FROM tb_stu WHERE sname like ‘%程序员’

SELECT * FROM tb_stu WHERE sname like ‘%PHP%’
```

 

### 3、查询日期型数据

```mysql
SELECT * FROM tb_stu WHERE date = ’2011-04-08′

注:不同数据库对日期型数据存在差异: ：

(1)MySQL:SELECT * from tb_name WHERE birthday = ’2011-04-08′

(2)SQL Server:SELECT * from tb_name WHERE birthday = ’2011-04-08′

(3)Access:SELECT * from tb_name WHERE birthday = #2011-04-08#
```

 

### 4、查询逻辑型数据

```mysql
SELECT * FROM tb_name WHERE type = ‘T’

SELECT * FROM tb_name WHERE type = ‘F’

逻辑运算符:and or not
 
```



### 5、查询非空数据

```mysql
SELECT * FROM tb_name WHERE address <>” order by addtime desc

注:<>相当于PHP中的!=
```

 

### 6、利用变量查询数值型数据

```mysql
SELECT * FROM tb_name WHERE id = ‘$_POST[text]‘

注:利用变量查询数据时，传入SQL的变量不必用引号括起来，因为PHP中的字符串与数值型数据进行连接时，程序会自动将数值型数据转变成字符串，然后与要连接的字符串进行连接
```

 

### 7、利用变量查询字符串数据

```mysql
SELECT * FROM tb_name WHERE name LIKE ‘%$_POST[name]%’

完全匹配的方法”%%”表示可以出现在任何位置
```

 

### 8、查询前n条记录

SELECT * FROM tb_name LIMIT 0,$N;

limit语句与其他语句，如order by等语句联合使用，会使用SQL语句千变万化，使程序非常灵活

 先排序后limit

### 9、查询后n条记录

SELECT * FROM tb_stu ORDER BY id ASC LIMIT $n

 

### 10、查询从指定位置开始的n条记录

SELECT * FROM tb_stu ORDER BY id ASC LIMIT $POST[begin],$n

注意:数据的id是从0开始的

 

### 11、查询统计结果中的前n条记录

SELECT * ,(yw+sx+wy) AS total FROM tb_score ORDER BY (yw+sx+wy) DESC LIMIT 0,$num

 

### 12、查询指定时间段的数据

SELECT 要查找的字段 FROM 表名 WHERE 字段名 BETWEEN 初始值 AND 终止值

SELECT * FROM tb_stu WHERE age BETWEEN 0 AND 18

 

### 13、按月查询统计数据

SELECT * FROM tb_stu WHERE month(date) = ‘$_POST[date]‘ ORDER BY date ;

注：SQL语言中提供了如下函数，利用这些函数可以很方便地实现按年、月、日进行查询

- year(data):返回data表达式中的公元年分所对应的数值

- month(data):返回data表达式中的月分所对应的数值

- day(data):返回data表达式中的日期所对应的数值

   

### 14、查询大于指定条件的记录

SELECT * FROM tb_stu WHERE age>$_POST[age] ORDER BY age;

###  

### 15、查询结果不显示重复记录

SELECT DISTINCT 字段名 FROM 表名 WHERE 查询条件

注:SQL语句中的DISTINCT必须与WHERE子句联合使用，否则输出的信息不会有变化 ,且字段不能用*代替

 

### 16、NOT与谓词进行组合条件的查询

(1)NOT BERWEEN … AND … 对介于起始值和终止值间的数据时行查询 可改成 <起始值 AND >终止值

(2)IS NOT NULL 对非空值进行查询

(3)IS NULL 对空值进行查询

(4)NOT IN 该式根据使用的关键字是包含在列表内还是排除在列表外，指定表达式的搜索，搜索表达式可以是常量或列名，而列名可以是一组常量，但更多情况下是子查询

 

### 17、显示数据表中重复的记录和记录条数

SELECT name,age,count(*) ,age FROM tb_stu WHERE age = ’19′ group by date

 

### 18、对数据进行降序/升序查询

SELECT 字段名 FROM tb_stu WHERE 条件 ORDER BY 字段 DESC 降序

SELECT 字段名 FROM tb_stu WHERE 条件 ORDER BY 字段 ASC 升序

注:对字段进行排序时若不指定排序方式，则默认为ASC升序

 

### 19、对数据进行多条件查询

SELECT 字段名 FROM tb_stu WHERE 条件 ORDER BY 字段1 ASC 字段2 DESC …

注意:对查询信息进行多条件排序是为了共同限制记录的输出，一般情况下，由于不是单一条件限制，所以在输出效果上有一些差别。

 

### 20、对统计结果进行排序

函数SUM([ALL]字段名) 或 SUM([DISTINCT]字段名),可实现对字段的求和，函数中为ALL时为所有该字段所有记录求和,若为DISTINCT则为该字段所有不重复记录的字段求和

如：SELECT name,SUM(price) AS sumprice FROM tb_price GROUP BY name

SELECT * FROM tb_name ORDER BY mount DESC,price ASC

 

### 21、单列数据分组统计

SELECT id,name,SUM(price) AS title,date FROM tb_price GROUP BY pid ORDER BY title DESC

注:当分组语句group by排序语句order by同时出现在SQL语句中时，要将分组语句书写在排序语句的前面，否则会出现错误。

 

### 22、多列数据分组统计

多列数据分组统计与单列数据分组统计类似

SELECT *，SUM(字段1*字段2) AS (新字段1) FROM 表名 GROUP BY 字段 ORDER BY 新字段1 DESC

SELECT id,name,SUM(price*num) AS sumprice FROM tb_price GROUP BY pid ORDER BY sumprice DESC

注：group by语句后面一般为不是聚合函数的数列，即不是要分组的列。

 

### 23、多表分组统计

SELECT a.name,AVG(a.price),b.name,AVG(b.price) FROM tb_demo058 AS a,tb_demo058_1 AS b WHERE a.id=b.id GROUP BY b.type;

