# MySQL

[TOC]

## 基础篇

### MySQL概述

|名称|全称|简称|
|:--:|:--:|:--:|
|数据库|存储数据的仓库，数据有组织的进行存储|DataBase（DB）|
|数据库管理系统|操纵和管理数据库的大型软件|DataBase Management System（DBMS）|
|SQL|操作关系型数据库的编程语言，定义了一套操作关系型数据库统一标准|Structured Query Language（SQL）|

- 主流的关系型数据库管理系统
  - Oracle
  - MySQL
  - SQL Server
  - PostgreSQL
  - MariaDB

- MySQL数据库下载：https://dev.mysql.com/downloads/windows/installer/8.0.html
- mysql数据库的启动与停止
    - 启动：net start mysql80
    - 停止：net stop mysql80
- 客户端连接
    - mysql [-h 127.0.0.1] [-P 3306] -u root -p

- 关系型数据库（RDBMS）
  - 概念：建立在关系模型的基础上，由多张相互连接的二维表组成的数据库
  - 特点：
    - 使用表存储数据，格式统一，便于维护
    - 使用sql语言操作，标准统一，使用方便

### SQL
#### sql通用语法
- SQL语句可以单行或者多行书写，以分号结尾
- SQL语句可以使用空格/缩进来增强语句的可读性
- MySQL数据库的sql语句不区分大小写，关键字建议使用大写
- 注释：
  - 单行注释：`--注释内容` 或 `#注释内容(MySQL独有)`
  - 多行注释：`/*注释内容*/`

#### sql分类

|分类|全称|说明|
|:--:|:--:|:--:|
|DDL|Data Definition Language|数据定义语言，用来定义数据库对象(数据库，表，字段)|
|DML|Data Manipulation language|数据操作语言用来对数据库表中的数据进行增删改|
|DQL|Data Query Language|数据控制语言，用来查询数据库中表的记录|
|DCL|Data control language|数据控制语言，用来创建数据库用户，控制数据库的访问权限|

#### MYSQL数据类型

MySQL中的数据类型有很多，主要分为三类：数字，字符串和日期时间类型

- 数值类型
![](./img/1.png)

- 字符串类型
![](./img/2.png)

- 日期时间类型
![](./img/3.png)

#### DDL

- 数据库操作

  ```sql
  -- 查询所有数据库
  SHOW DATABASES;

  -- 查询当前数据库
  SELECT DATABASE();

  -- 创建
  CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET utf8mb4] [COLLATE 排序规则]

  -- 删除
  DROP DATABASE [IF EXISTS] 数据库名

  -- 使用
  USE 数据库名
  ```

- 表操作

  ```sql
  -- 查询当前数据库所有表
  SHOW TABLES;

  -- 查询表结构
  DESC 表名;

  -- 查询指定表的建表语句
  SHOW CREATE TABLE 表名;

  -- 创建 int date varchar(10)
  CREATE TABLE 表名(
    字段1 类型 [COMMENT 字段1注释],
    字段2 类型 [COMMENT 字段2注释],
    字段3 类型 [COMMENT 字段3注释]
  )[COMMENT 表注释];
  ```

- 修改表

  ```sql
  -- 添加字段
  ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];

  -- 修改数据类型
  ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);

  -- 修改字段名和字段类型
  ALTER TABLE 表名 CHANGE 旧字段名 类型(长度) [COMMENT 注释] [约束];

  --删除字段
  ALTER TABLE 表名 DROP 字段名;

  -- 修改表名
  ALTER TABLE 表名 RENAME TO 新表名;

  -- 删除表
  DROP TABLE [IF EXISTS] 表名;

  -- 删除指定表 并重新创建该表
  TRUNCATE TABLE 表名;
  ```

#### DML

- DML英文全称是Data Manipulation Language(数据操作语言)，用来对数据库中标的数据记录进行增删改操作
- 添加数据(INSERT)
  ```sql
  -- 1.给指定字段添加数据
  INSERT INTO 表名 (字段名1, 字段名2,...) VALUES (值1,值2);
  -- 2.给全部字段添加数据
  INSERT INTO 表名 VALUES (值1, 值2);
  -- 3.批量添加数据
  INSERT INTO 表名 (字段1,字段2) VALUES (值1,值2),(值1,值2),(值1,值2);
  INSERT INTO 表名 VALUES (值1,值2),(值1,值2),(值1,值2);
  ```
- 修改数据(UPDATE)
  ```SQL
  -- 基本语法
  UPDATE 表名 SET 字段名1=值1, 字段名2=值2,... [WHERE 条件];
  ```
- 删除数据(DELETE)
  ```sql
  DELECT FROM 表名 [WHERE 条件]
  ```

#### DQL

- DQL英文全称是Data Query Language(数据查询语言)，用来查询数据库中表的记录

- 语法
  ```sql
  SELECT 
    字段列表
  FROM
    表名列表
  WHERE
    条件列表
  GROUP BY
    分组字段列表
  HAVING
    分组后条件列表
  ORDER BY
    排序字段列表
  LIMIT
    分页参数;
  ```

- 基本查询
  ```sql
  -- 查询多个字段
  SELECT 字段,字段,字段 FROM 表名;
  SELECT * FROM 表名; --查询全部字段

  -- 设置别名
  SELECT 字段 AS 别名, 字段 AS 别名 FROM 表名; --AS可以省略
  SELECT 表别名.字段 AS 别名, 表别名.字段 AS 别名 FROM 表名 AS 表别名;

  -- 取出重复记录
  SELECT DISTINCT 字段列表 FROM 表名;
  ```

- 条件查询
  ```sql
  SELECT 字段列表 FROM 表名 WHERE 条件列表;
  ```
  条件：
  ![](./img/4.png)

- 聚合函数
  - 将一列数据作为一个整体，进行纵向计算
  - 常见聚合函数
    - count：统计数量
    - max：最大值
    - min：最小值
    - avg：平均值
    - sum：求和
  - 语法：
    ```SQL
    SELECT 聚合函数(字段列表) FROM 表名;
    ```
  - 注意：所有聚合函数是不计算null值的

- 分组查询
  - 语法：
    ```sql
    SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件];
    ```
  - WHERE与having区别
    - 执行机制不同，where是分组之前进行过滤，不满足where条件，不参与分组，而having是分组之后对结果进行过滤
    - 判断调经不同，where不能对聚合函数进行判断，而having可以
  - 例子
    ```sql
    -- 根据性别分组, 根据男女员工数量
    SELECT sex,COUNT(*) FROM employee GROUP BY sex;
    -- 根据性别分组，根据男员工和女员工的平均年龄
    SELECT sex,avg(age) FROM employee GROUP BY sex;
    -- 查询年龄小于45的员工，并根据工作地区分组，获取员工数量大于等于3的工作地址
    SELECT workaddress, count(*) FROM employee WHERE age<=45 GROUP BY workaddress HAVING count(*)>=3;
    ```

- 排序查询
  - 语法
    ```sql
    SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1, 字段2 排序方式2;
    ```
  - 排序方式
    - ASC:升序默认值
    - DESC：降序
    - 如果多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序
  - 案例
    ```sql
    -- 根据年龄进行升序排序
    SELECT  * FROM employee ORDER BY age ASC ;
    -- 根据年龄进行降序排序
    SELECT * FROM employee ORDER BY age DESC;
    -- 根据年龄进行升序排，如果年龄相同，按照入职时间降序
    SELECT * FROM employee ORDER BY age ASC, emptime DESC;
    ```

- 分页查询
  - 语法：
    ```sql
    SELECT 字段列表 FROM 表名 LIMIT 起始索引 查询记录数;
    ```
  - 注意：
    - 起始索引是从0开始，起始索引=(查询页码-1)*每页显示记录数
    - 分页查询是数据库的方言，不同的数据库有不同的实现，mysql中是LIMIT
    - 如果查询的是第一页数据，起始索引可以省略，直接可以写`LIMIT 10`
  - 案例
    ```sql
    -- 查询前10条数据
    SELECT * FROM employee LIMIT 0,10;
    -- 查询第二页数据
    SELECT * FROM employee LIMIT 10,10;
    ```

- DQL执行顺序
  ![](./img/5.png)

#### DCL

- DCL英文全称是Data Control Language(数据控制语言)，用来管理数据库用户、控制数据库的访问权限

- 管理用户
  ```sql
  -- 查询用户
  USE mysql;
  SELECT * FROM user;

  -- 创建用户 %表示任意主机
  CREATE USER `用户名`@`主机名` IDENTIFIED BY `密码`;

  -- 修改用户密码
  ALTER USER `用户名`@`主机名` IDENTIFIED WITH mysql_native_password BY `新密码`;

  -- 删除用户
  DROP USER `用户名`@`主机名`;
  ```

- 权限控制
  - mysql汇总定义了很多种权限，但是常用的就以下几种
  ![](./img/6.png)

```sql
-- 查询权限
SHOW GRANTS FOR '用户名'@'主机名';

-- 授予权限
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';

-- 撤销权限
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```

### 函数

- 函数是指一段可以直接被另一段程序调用的程序或者代码

- 字符串函数
  - MySQL中内置了很多字符串函数，常用的几个如下
    ![](./img/7.png)

- 数值函数
  - 常见的数值函数如下：
    ![](./img/8.png)

- 日期函数
  - 常见的日期函数如下：
    ![](./img/9.png)

- 流程控制函数
  - 流程函数也是很常用的一类函数，可以在SQL中实现条件筛选，从而提高语句的效率
    ![](./img/10.png)

### 约束

- 概述
  - 约束是作用于表中字段上的规则，用于限制存储在表中的数据
  - 目的：保证数据库中数据的正确、有效性和完整性
  - 约束是作用于表中字段上的，可以在创建表/修改表的时候添加约束

- 分类
  ![](./img/11.png)
- 案例
  ![](./img/12.png)
  ```sql
  -- 创建表
  CREATE TABLE user(
    id INT PRIMARY KEY AUTO_INCREMENT COMMENT '主键',
    name VARCHAR(10) NOT NULL UNIQUE COMMENT '姓名',
    age INT CHECK(age>0 && age<=120) COMMENT '年龄',
    seatus CHAR(1) DEFAULT '1' COMMENT '状态',
    gender char(1) COMMENT '性别'
  ) COMMENT '用户表';
  -- 插入数据
  INSERT INTO user
    (name,age,seatus,gender) 
  VALUES 
    ('Ton1',19,'1','男'), 
    ('Ton2',34,'0','男');
  ```

- 外键约束
  - 外键用来让两张表的数据之间建立链接，从而保证数据的一致性和完整性
  ![](./img/13.png)
  - 目前上述的两张表，在数据库层面，并未建立外键关联，所以是无法保证数据的一致性和完整性的
  - 添加外键
    ```sql
    CREATE TABLE 表名(
      字段名 数据类型
      [CONSTRAINT] [外键名称] FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名)
    );
    ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名);
    ```
  - 删除外键
    ```sql
    ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
    ```
- 外键的删除/更新行为
  ![](./img/14.png)
  ```sql
  ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段) REFERENCES 主表名(主表字段名) ON UPDATE ON DELETE CASCADE;
  ```

### 多表查询

- 多表关系
  - 项目开发中，在进行数据库表结构设计时，会根据业务需求以及业务模块之间的关系，分析并设计表结构，由于业务之间相互关联，所以各个表结构之间也存在着各种联系，基本上分为三种：
    - 一对多(多对一)
    - 多对多
    - 一对一
  - 一对多(多对一)
    - 案例：部门与员工的关系
    - 关系：一个部门对应多个员工，一个员工对应一个部门
    - 实现：在多的一方建立外键，指向的一的一方的主键
  - 多对多
    - 案例：学生与课程的关系
    - 关系：一个学生可以选修多门课程，一门课程也可以供多个学生选择
    - 实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键
  - 一对一
    - 案例：用户与用户详情的关系
    - 关系：多用于单表拆分，将一张表的基础字段放在一张表中，其他详细字段放在另一张表中，以提升操作效率
    - 实现：在任意一方加入外键，关联另一方的主键，并且设置外键为唯一的(UNIQUE)

- 多表查询概述
  - 指从多张表中查询数据
  - 笛卡尔积：笛卡尔乘积是指在数学中，两个集合A和B的所有组合情况(在多表查询中，需要消除无效的笛卡尔积)
    ![](./img/15.png)
  ```SQL
  SELECT * FROM emp, dept; --有无效的笛卡尔积情况
  SELECT * FROM emp, dept WHERE emp.dept_id = dept.id; --消除笛卡尔积
  ```

- 多表查询的分类
  - 连接查询
    - 内连接：相当于查询A、B交集部分数据
    - 外连接：
      - 左外连接：查询左表所有数据，以及两张表交集部分的数据
      - 右外连接：查询右表所有数据，以及两张表交集部分的数据
    - 自连接：当前表与自身的链接查询，自连接必须使用表列名
  - 子查询

- 内连接
  - 隐式内连接
    ```sql
    SELECT 字段列表 FROM 表1,表2 WHERE 条件...;
    ```
  - 显式内连接
    ```sql
    SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件...;
    ```

- 外连接
  - 左外连接
    ```sql
    SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件;
    ```
    - 相当于查询表1的所有数据包含表1和表2交集部分的数据
  - 左外连接
    ```sql
    SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件;
    ```
    - 相当于查询表2的所有数据包含表1和表2交集部分的数据

- 自连接
  - 自连接查询，可以是内连接查询，也可以是外连接查询
  ```sql
  SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件;
  ```

- 联合查询-union, union all
  - 对于union查询，就是把多次查询的结果合并起来，形成一个新的查询结果集
  ```sql
  SELECT 字段列表 FROM 表A;
  UNION [ALL]
  SELECT 字段列表 FROM 表B;
  ```
  - 对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致
  - union all会将全部的数据直接合并到一起，union会对合并之后的数据去重

### 事务