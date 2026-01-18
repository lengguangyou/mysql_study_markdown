# 数据分析DAY05

## 1.多表操作（接DAY04）

### 	1.1. 子查询

- 子查询作为条件

```sql
SELECT * FROM products WHERE price > (SELECT AVG(price) FROM products);
```

- 子查询作为临时表

```sql
SELECT * FROM (SELECT id,AVG(price) FROM products GROUP BY id);
```

- 子查询作为字段

```sql
SELECT id,(SELECT price FROM products) FROM products;
```

## 2.快速建表

### 	2.1 快速建表

```sql
CREATE TABLE 数据库名.表名 LIKE 源数据库名.表名;
```

### 	2.2 快速插入数据

```SQL
INSERT INTO 数据库名.表名 SELECT * FROM 源数据名.表名;
```

### 	2.3 复制表的同时插入数据

```SQL
CREATE TABLE 数据库名.表名 AS SELECT * FROM 源数据名.表名;
```

## 3.内置函数

### 	3.1 数值函数

- ***ROUND(X,N*)** 对X进行四舍五入并保留N位小数，N默认为0

- ***FORMAT(X,N)*** 对X进行四舍五入并保留N位小数，以##，###，###格式显示

- ***FLOOR(X)*** 向下取整

- ***CEIL(X)*** 向上取整

- ***MOD(X,Y)*** 求X除以Y的余数

- ***POW(X,Y)*** 求X的Y次方

- ***RAND()*** 返回0~1的随机数

### 3.2 字符串函数

- ***LOWER(字符串)*** ：转换为小写

- ***UPPER(字符串)***： 转换为大写

- ***REVERSE(字符串)*** ：反转字符串

- ***REPEAT(字符串,N)*** ：字符串重复N次

- ***CONCAT(字符串1,,字符串2)*** ：字符串拼接

- ***CONCAT_WS(分隔符,字符串1,字符串2)***：指定分隔符拼接

- ***REPLACE(字符串1,字符串2)***：字符串替换

- ***SUBSTR(字符串,N,M)***：从字符串的第N个字符（非字符索引）往后截取M个字符

- ***LEFT(字符串,N)***：从字符串左侧截取N个字符

- ***RIGHT（字符串,N）***：从字符串右侧截取N个字符

- ***CHAR_LENGTH(字符串)***：字符串长度

- ***LENGTH(字符串)***：字符串的字节长（一个中文或中文符号占3个字节）

### 3.3 日期函数

  	日期类型：DATE：2025-01-01,TIME：12:00:00,DATETIME：2025-01-01 		12:00:00,TIMESTAMP：显示格式与DATETIME相同，但TIMESTAMP以时间戳（1970-1-1 00:00:00 到现在的秒数）存储

- ***CURRENT_DATE()***：获取DATE类型时间

- ***CURRENT_TIME()***：获取TIME类型时间

- ***NOW()***：获取DATETIME类型时间

- ***CURRENT_TIMESTAMP***：获取时间戳

- ***DATE_ADD('时间',INTERVAL N DAY)***：N天后的时间

- ***DATE_SUB('时间',INTERVAL N DAY)***：N天前的时间

- ***DATEDIFF('时间1'，'时间2')***：两个时间日期的天数差

- ***TIMESTAMPDIFF(时间单位，时间1，时间2)***：时间差自定义单位（MONTH,DAY,……）

- ***YEAR(时间)***：获取时间的年份

- ***MONTH(时间)***：获取时间的月份

- ***DAY(时间)***：获取时间的日

- ***HOUR(时间)***：获取时间的小时

- ***MINUTE(时间)***：获取时间的分钟

- ***SECOND(时间)***：获取时间的秒

- ***WEEKDAY(时间)***：计算星期几

- ***DATE_FORMAT(时间，‘转换格式’)***：

  %Y：2025   %y：25

  %M：September   %m：09

  %D：10th   %d：10

  %H：24小时制   %h：12小时制

  %i：分   %s：秒

- ***STR_TO_DATE(时间，时间格式)***：字符串转时间

- ***UNIX_TIMESTAMP(时间)***：时间或字符串转时间戳

- ***FROM_UNIXTIME(时间戳，时间格式)***：时间戳转字符串

### 3.4 流程控制

#### 3.4.1 CASE WHEN

```SQL
SELECT 
	CASE
		WHEN 条件 THEN 值
		WHEN 条件 THEN 值
		……
		ELSE 值
	END
FROM USER;
```

#### 3.4.2 IF(条件,值1，值2)

满足条件返回值1，否则返回值2

#### 3.4.3 IFNULL(值1，值2)

值1不为空时返回值1，否则返回值2

## 4.多行变一行

![屏幕截图 2026-01-07 202924](D:\HeimaAiTxt\MdText\mdPhoto\屏幕截图 2026-01-07 202924.png)


![屏幕截图 2026-01-07 203206](D:\HeimaAiTxt\MdText\mdPhoto\屏幕截图 2026-01-07 203206.png)

## 5.一行变多行

![屏幕截图 2026-01-07 202937](D:\HeimaAiTxt\MdText\mdPhoto\屏幕截图 2026-01-07 202937.png)

![屏幕截图 2026-01-07 203221](D:\HeimaAiTxt\MdText\mdPhoto\屏幕截图 2026-01-07 203221.png)

