# 数据分析DAY04

## 1.SQL执行顺序

FROM=>WHERE=>GROUP BY=>聚合=>HAVING=>SELECT=>ORDER BY=>LIMIT

## 2.多表操作

### 2.1表关系

一对多，多对多，一对一

### 2.2 外键和约束

外键FOREIGN KEY

添加:

```SQL
CREATE TABLE t1(
id INT PRIMARY KEY,
……
)；
CREATE TABLE t2(
id INT PRIMARY KEY,
……
CONSTRAINT FOREIGN KEY (id) REFERENCES t1(id)
)；
```

删除:

```SQL
ALTER TABLE 表名 DROP FOREIGN KEY 外键约束名;
```

建表后添加:

```SQL
ALTER TABLE 表名 ADD CONSTRAINT 外键约束名 FOREIGN KEY (从表外键字段) REFERENCES 主表名(主键);
```

### 2.3关联查询

#### 2.3.1 笛卡尔积（交叉连接/无条件连接）

左表与右表每一行关联

```SQL
SELECT * FROM 表1 JOIN 表2;
#或者
SELECT * FROM 表1,表2;
```

#### 2.3.2 内连接 INNER JOIN

两表关联时，满足关联条件的数据才显示

```SQL
SELECT 字段1，字段2…… FROM 左表名 INNER JOIN 右表名 ON 关联条件;
#例:
SELECT c.id,c.name,p.id,p.name FROM c INNER JOIN p ON c.id = p.category_id;
```

隐式连接:

```SQL
SELECT 字段1，字段2 FROM 表1，表2 WHERE 关联条件; 
```

#### 2.3.3 左外连接

两表关联时，显示满足关联条件的数据的同时·，还会保留显示左表不满足条件的数据，没有的部分用NULL填充

```SQL
SELECT 字段1，字段2…… FROM 左表名 LEFT JOIN 右表名 ON 关联条件;
```

#### 2.3.4 右外连接

两表关联时，显示满足关联条件的数据的同时·，还会保留显示右表不满足条件的数据，没有的部分用NULL填充

```SQL
SELECT 字段1，字段2…… FROM 左表名 RIGHT JOIN 右表名 ON 关联条件;
```

#### 2.3.5 全连接

两表关联时，显示满足关联条件的数据的同时·，还会保留显示左右表不满足条件的数据，没有的部分用NULL填充

```SQL
#去重，也可使用UNION DISTINCT
SELECT 字段1，字段2…… FROM 左表名 LEFT JOIN 右表名 ON 关联条件
UNION
SELECT 字段1，字段2…… FROM 左表名 RIGHT JOIN 右表名 ON 关联条件;
#不去重(两表同时满足条件的数据会显示两遍)
SELECT 字段1，字段2…… FROM 左表名 LEFT JOIN 右表名 ON 关联条件
UNION ALL
SELECT 字段1，字段2…… FROM 左表名 RIGHT JOIN 右表名 ON 关联条件;
```

#### 2.3.6 自关联

关联时，两表为同一张表

```SQL
SELECT * FROM 表 别名1 JOIN 表 别名2 ON 关联条件;#自关联必须起别名
```

