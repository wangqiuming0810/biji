sql语句不区分大小写。



# SQL SELECT 语句

```mysql
SELECT column_name,column_name
FROM table_name;
```

# SQL SELECT DISTINCT 语句

```
SELECT DISTINCT column_name,column_name
FROM table_name;
```



#  AND & OR

逻辑运算符和其他语言基本类似相通



# order by

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。



# SQL INSERT INTO 语句

```
INSERT INTO Websites (name, url, alexa, country)
VALUES ('百度','https://www.baidu.com/','4','CN');
```



# LIKE 子句

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。



# SQL IN 操作符

------

## IN 操作符

IN 操作符允许您在 WHERE 子句中规定多个值。

### SQL IN 语法

```
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...);
```

```
SELECT * FROM Websites
WHERE name IN ('Google','菜鸟教程');
```



# SQL BETWEEN 操作符

------

BETWEEN 操作符用于选取介于两个值之间的数据范围内的值。

------

## SQL BETWEEN 操作符

BETWEEN 操作符选取介于两个值之间的数据范围内的值。这些值可以是数值、文本或者日期。

### SQL BETWEEN 语法

```
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN  value1 AND value2;
```

```
SELECT * FROM Websites
WHERE alexa BETWEEN 1 AND 20;
```

