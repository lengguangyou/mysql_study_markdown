# 数据分析DAY03

## 1.数据类型

整数:tinyint[-127~128],tinyint unsigned[0~255],int[-2^31~2^31],bigint

小数:float,double,decimal(整数位和小数位位数,小数位数)

字符串:char(25)[定长字符串],varchar[不定长字符串],text[长文本,如新闻]

日期:data[日期],time[时间],year[年],timestamp[年-月-日 时-分-秒]

```sql
CURRENT_TIMESTAMP()#当前时间 年月日时分秒
CURRENT_TIMEDATA()
CURRENT_TIMETIME()
```

## 2.数据约束

### 2.1 主键primary key

#### 2.1.1 作用及用法

唯一标识且非空

```SQL
CREATE TABLE PERSON(
id INT PRIMARY KEY,
……
)；
```

#### 2.1.2 自动增长AUTO_INCREMENT

```SQL
CREATE TABLE PERSON(
id INT PRIMARY KEY AUTO_INCREMENT,
……
)；
```

### 2.2 必须有值NOT NULL

null表示未知和不存在

null ！= ''

```
CREATE TABLE PERSON(
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
……
)；
```



### 2.3 唯一UNIQUE

不能重复

```
CREATE TABLE PERSON(
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50) UNIQUE,
……
)；
```



### 2.4 默认值DEFAULT

默认值

```
CREATE TABLE PERSON(
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50) DEFAULT '未知姓名',
……
)；
```



### 2.5 外键FOREIGN KEY

主表关联从表

## 3.DQL(数据查询语言)

### 3.1 简单查询

![屏幕截图 2026-01-03 121723](D:\HeimaAiTxt\MdText\mdPhoto\屏幕截图 2026-01-03 121723.png)

distinct去重

```sql
SELECT DISTINCT id FROM products;
```

### 3.2 条件查询

#### 3.2.1 语法

```SQL
SELECT * FROM 表名 WHERE 条件;
```

#### 3.2.2 条件运算符

=,>,<,<=,>=,!=,<>

AND,OR,NOT,IN,LIKE(%表示任意多个字符，_表示单个字符),IS NULL,IS NOT NULL

BETWEEN……AND……

### 3.3 排序查询

```
SELECT * FROM stu ORDER BY score DESC;降序
SELECT * FROM stu ORDER BY score ASC;#升序
SELECT * FROM stu ORDER BY score ASC,id DESC;#多排序条件
```

### 3.4 聚合函数

计数：COUNT(字段名),最大值：MAX(字段名),最小值：MIN(字段名),求和：SUM(字段名),取平均：AVG(字段名)

```SQL
SELECT COUNT(id) FROM stu；
```

### 3.5 分组查询

语法：

```SQL
SELECT 分组字段，聚合函数，…… FROM 表名 GROUP BY 分组字段,……;
```

分组过滤：

```SQL
SELECT 分组字段，聚合函数，…… FROM 表名 GROUP BY 分组字段,…… HAVING 条件表达式;
```

### 3.6 LIMIT 查询

```SQL
SELECT * FROM products
	ORDER BY price DESC
	LIMIT 0,3;#limit 起始索引，单页条数
```

