## 数据分析day06

## 1.窗口函数

在不改变结果及行数的情况下，对多行数据进行计算

### 1.1 基础语法

```
SELECT 字段，……，<window function> OVER (……) FROM 表名
```

### 1.2 PARTITION分组

对整张表数据分组，供窗口函数使用

```
SELECT 字段，……，<window function> OVER (PARTITION BY 字段，……) FROM 表名
```

### 1.3 排名函数

- ***RANK()***并列，不连续的排序序号，例123356
- ***DENSE_RANK()***并列，连续的排序序号，例123345
- ***ROW_NUMBER()***不并列，唯一序号，例123456

语法示例：

```
SELECT name,coure,score,RANK() OVER (ORDER BY score DESC) AS score_rank FROM tb_score;
```

### 1.4 CTE公共表达式

子查询充当数据源，进一步进行查询操作

语法：

```
WITH 子查询1别名 AS (子查询1语句),子查询2别名 AS (子查询2语句) SELECT …… FROM 上方的子查询别名；
```

### 1.5 NTILE分桶函数

将每个分区数据均分成X组，多出来的会从上到下逐步均分，例3,3,2,2

语法示例：

```
SELECT id,views,NTILE(4) OVER (ORDER BY views DESC) AS 'qua' FROM auction;
```

### 1.6 LAG和LEAD函数

- LAG(字段,N,M)返回分区中，相对于当前行的前N行指定字段内容，如没有则返回M
- LEAD(字段,N,M)返回分区中，相对于当前行的后N行指定字段内容，如没有则返回M
- 注意:M和N可以省略，N默认1，M默认NULL

## 2.MYSQL拓展

### 2.1 存储引擎

查看语法

```
SHOW ENGINES;
```

建表时指定存储引擎

```
CREATE TABLE tab (id INT PRIMARY KEY,name VARCHAR(100)) ENGINE=InnoDB;
```



|             INNODB             |               MYISAM               |
| :----------------------------: | :--------------------------------: |
|            支持事务            |             不支持事务             |
|            支持外键            |             不支持外键             |
|  行级锁（防止同时修改同一行）  |    表级锁（防止同时修改同一表）    |
| 聚集索引（索引与内容是一体的） |  非聚集索引（数据与内容是分离的）  |
|      COUNT(*)需要实时计算      | COUNT(*)查全表总数快，直接存放总数 |

### 2.2 事务

一组sql操作的集合，要么都成功，要么都失败

**流程：**

开启事务

```
START TRANSCATION;
```

事务

```
sql语句1；sql语句2；……
```

有无异常

```
COMMIT;没有异常，提交
ROLLBACK;有异常，回滚
```

单条sql语句有数据库自动管理（隐式事务），背后执行BEGIN->执行SQL->COMMIT,如果语句执行失败，自动执行ROLLBACK

查看事务状态

```
SELECT @@autocommit；#1:自动提交，0：禁用
```

禁用自动提交

```
SET autocommit=0#为1时取消禁用
```

并发问题与隔离级别

- 脏读：读到了别人还没确认的，可能撤回的草稿
- 不可重复的：两次读同一份数据，中间被人更改，结果不同
- 幻读：两次统计总数，中间被人增加或删除了一条数据，总数变化

隔离级别

| 读未提交 |                    啥都不防                    |
| :------: | :--------------------------------------------: |
| 读已提交 |                     防脏读                     |
| 可重复读 | 防脏读和不可重复读，配合间隙锁一定程度避免幻读 |
|  串行化  |             杜绝所以问题但性能最差             |

### 2.3 索引

#### 2.3.1 索引分类

- 主键索引

- 唯一索引

- 普通索引（index）

WHERE column = 'value'查询机制B-tree

```
CREATE INDEX 索引名 ON 表名(字段名);
```

- 全文索引(FULLTEXT)

MATCH(column) AGAINST('query')查询机制倒序索引加分词

```
CREATE FULLTEXT 索引名 ON 表名（字段名）;
```

#### 2.3.2 索引操作

- 查看所有索引

```
SHOW INDEX FROM users;
```

- 删除索引

```
DROP INDEX idx_age ON users;
```

- 添加索引

```
CREATE INDEX idx_age ON users(age);
```

- 添加联合索引

```
CREATE INDEX idx_age ON users(city,age);
```

### 2.4 视图

sql语句获取动态的数据集,原表数据改变会影响视图数据

- 创建视图

```
CREATE VIEW 视图名 AS SELECT 字段1，字段2，…… FROM 数据库名.数据库表名;
```

- 查看视图

```
SELECT * FROM 视图名;#查看视图

SHOW FULL TABLES;#查看所有视图和表

DESC 视图名;#查看视图字段信息
```

- 修改视图

```
ALTER VIEW 视图名 AS SELECT 字段1，字段2，…… FROM 数据库名.数据库表名 WHERE 条件;#修改视图数据

RENAME TABLE 视图名 TO 新视图名;
```

- 删除视图

```
DROP VIEW 视图名;
```

### 2.5 ER模型

实体型（矩形表示），属性（椭圆表示），联系（菱形表示）

![屏幕截图 2026-01-10 194904](D:\HeimaAiTxt\MdText\mdPhoto\屏幕截图 2026-01-10 194904.png)

### 2.6 三范式

- 第一范式：列不能够再分为其他几列

- 第二范式：表必须有一个主键

- 第三范式：非主键必须直接依赖于主键，不能存在依赖传递