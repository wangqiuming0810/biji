## 连接到Mysql服务（MySQL数据库）的指令

切换到MySQL的路径

```
cd /D 路径
```

```mysql
mysql -u root -p
Enter password：123456
```

首先要保证MySql是运行的状态，

```c
net start mysql
```



连接的指令：

```mysql
mysql -h 主机IP -P 端口 -u -root -p密码
```

**注：**

- -p后面的密码没有空格
- -p后面没有写密码，回车会要求输入密码
- 如果没有写-h主机，默认就是本机
- 如果没有写-P端口，默认就是3306，是my.ini里面那个端口。
- 在实际中3306 ，一般修改。



## 命令行执行



**创建数据库**

```
create DATABASE 数据库的名字
```



**删除数据库**

````
drop DATABASE 数据库的名字
````



**选择数据库**

```
use 数据库名
```



**创建数据表**

````sql
root@host# mysql -u root -p
Enter password:*******
mysql> use RUNOOB;
Database changed
mysql> CREATE TABLE runoob_tbl(
   -> runoob_id INT NOT NULL AUTO_INCREMENT,
   -> runoob_title VARCHAR(100) NOT NULL,
   -> runoob_author VARCHAR(40) NOT NULL,
   -> submission_date DATE,
   -> PRIMARY KEY ( runoob_id )
   -> )ENGINE=InnoDB DEFAULT CHARSET=utf8; 存储引擎、字符集
Query OK, 0 rows affected (0.16 sec)
mysql>
````



**删除数据表**

```mysql
先选择数据库
DROP TABLE 表的名字;
```



**插入数据**

以下为向MySQL数据表插入数据通用的 **INSERT INTO** SQL语法：

```mysql
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```

例如：

```mysql
root@host# mysql -u root -p password;
Enter password:*******
mysql> use RUNOOB;
Database changed
mysql> INSERT INTO runoob_tbl 
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("学习 PHP", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
mysql> INSERT INTO runoob_tbl
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("学习 MySQL", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
mysql> INSERT INTO runoob_tbl
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("JAVA 教程", "RUNOOB.COM", '2016-05-06');
Query OK, 1 rows affected (0.00 sec)
mysql>
```



**读取数据表**

```mysql
select * from table_name;
```



**查询数据表**

```mysql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
```



**SQL SELECT WHERE 子句**

```mysql
SELECT * from runoob_tbl WHERE runoob_author='菜鸟教程';
```



**MySQL 的 WHERE 子句的字符串比较是不区分大小写的。 你可以使用 BINARY 关键字来设定 WHERE 子句的字符串比较是区分大小写的。**

```mysql
SELECT * from runoob_tbl WHERE BINARY runoob_author='runoob.com';
```

**更新语句**

```mysql
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

例如：

```mysql
mysql> UPDATE runoob_tbl SET runoob_title='学习 C++' WHERE runoob_id=3;
Query OK, 1 rows affected (0.01 sec)
 
mysql> SELECT * from runoob_tbl WHERE runoob_id=3;
+-----------+--------------+---------------+-----------------+
| runoob_id | runoob_title | runoob_author | submission_date |
+-----------+--------------+---------------+-----------------+
| 3         | 学习 C++   | RUNOOB.COM    | 2016-05-06      |
+-----------+--------------+---------------+-----------------+
1 rows in set (0.01 sec)
```

**删除语句**

```MySQL
ELETE FROM table_name [WHERE Clause]
```

- 如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除。
- 你可以在 WHERE 子句中指定任何条件
- 您可以在单个表中一次性删除记录。

当你想删除数据表中指定的记录时 WHERE 子句是非常有用的。

例如：

```mysql
mysql> use RUNOOB;
Database changed
mysql> DELETE FROM runoob_tbl WHERE runoob_id=3;
Query OK, 1 row affected (0.23 sec)
```



**MySQL LINK子句**

```mysql
SELECT field1, field2,...fieldN 
FROM table_name
WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue'
```

相当于查找子串，

- 你可以在 WHERE 子句中指定任何条件。
- 你可以在 WHERE 子句中使用LIKE子句。
- 你可以使用LIKE子句代替等号 **=**。
- LIKE 通常与 **%** 一同使用，类似于一个元字符的搜索。
- 你可以使用 AND 或者 OR 指定一个或多个条件。
- 你可以在 DELETE 或 UPDATE 命令中使用 WHERE...LIKE 子句来指定条件。

例如：

查找姓刘的学生

```mysql
SELECT *
FROM student
WHERE Sname not LIKE '刘%';
```

姓王且名字为三个字

```mysql
SELECT * FROM student WHERE Sname like '王__';
```



## MySQL   UNION操作符

可以选出重复的元素，连接两个select语句，将选中的元素一起显示，默认去除重复的元素。



**语法**

```mysql
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```

**演示数据库**

下面是选自 "Websites" 表的数据：

```mysql
SELECT country FROM Websites
UNION
SELECT country FROM apps
ORDER BY country;
```

**不保留重复的属性。**

下面是 "apps" APP 的数据：

```mysql
SELECT country FROM Websites
UNION ALL
SELECT country FROM apps
ORDER BY country;
```

保留重复的属性

**SQl语句排序**



```mysql

```

