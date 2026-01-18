# 数分DAY02

## 1、数据库

### 1.1、概念

存储和管理数据的系统

### 1.2、特点

高效存储、快速检索、维护安全、保证一致性

### 1.3、功能

增加、修改、删除、查询

### 1.4、分类

关系型数据库、非关系型数据库

## 2、sql语句（结构化查询语言）

### 2.1、分类

DDL、DML、DQL、DCL

### 2.2、DDL（数据定义语音）

#### 2.2.1、数据库操作

创建数据库：

```sql
#创建数据库
CREATE DATABASE 数据库名;
#当数据库不存在时创建
CREATE DATABASE IF NOT EXISTS 数据库名;
#创建数据库并指定字符集utf8
CREATE DATABASE 数据库名 CHARSET='utf8';
```

查看所有数据库：

```sql
SHOW DATABASES;
```

使用数据库：

```sql
USE 数据库名;
```

查看当前选择的数据库：

```sql
SELECT database();
```

删除数据库：

```sql
DROP DATABASE 数据库名;
```



#### 2.2.2、数据库表操作

创建数据表：

```sql
CREATE TABLE 数据库表名(
    字段名 字段类型 字段约束，
    字段名 字段类型 字段约束，
    字段名 字段类型 字段约束，
    ……
);
```

查看所有数据表：

```sql
SHOW TABLES;
```

查看指定表结构：

```sql
DESC 数据库表名;
```

修改表名：

```sql
RENAME TABLE 数据表名 TO 数据库新表名;
```

删除表：

```sql
DROP TABLE 数据库表名;
```

添加表字段：【***如果字段名与关键字相同，需要在字段两边加````,如``desc】

```sql
ALTER TABLE 表名 ADD 字段名 字段类型 字段约束;
```

修改表字段：

```sql
ALTER TABLE 表名 CHANGE 字段名 新字段名 字段类型 字段约束;
```

删除表字段：

```sql
ALTER TABLE 表名 DROP字段名;
```



### 2.3、DML

插入数据：

```sql
#不指定字段，一次插入一条
INSERT INTO 表名 VALUES(值1,值2,值3……);
#不指定字段，一次插入多条
INSERT INTO 表名 VALUES(值1,值2,值3……),(值1,值2,值3……),……;
#指定字段，一次插入一条
INSERT INTO 表名(字段1,字段2,字段3) VALUES(值1,值2,值3……);
#指定字段，一次插入多条
INSERT INTO 表名(字段1,字段2,字段3) VALUES(值1,值2,值3……),(值1,值2,值3……),……;
```

更新数据：

```sql
#更新所有行
UPDATE 表名 SET 字段名=值1,字段名=值2,……;
#更新满足条件的行
UPDATE 表名 SET 字段名=值1,字段名=值2,…… WHERE 条件;
```

删除数据：

```sql
#删除所有表中数据（主键自增不清零）
DELETE FROM 表名;
#删除满足条件的表中数据
DELETE FROM 表名 WHERE 条件;
#删除所以表中数据（主键自增清零）
TRUNCATE TABLE 表名;
```

