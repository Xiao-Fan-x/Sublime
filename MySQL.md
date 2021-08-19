创建用户：create USER 用户名@IP地址 IDENTIFIED BY '密码' //指定IP地址

CREATE USER 用户名@'%' IDENTIFIED BY '密码'

授予用户权限

GRANT 权限1,权限2,权限3... ON 数据库.* TO 用户名@IP地址

撤销用户权限：

REVOKE 权限1,权限2,权限3... ON 数据库.* FROM 用户名@IP地址

查看用户权限：

SHOW GRANTS FOR 用户名@IP地址

删除用户：

DROP USER 用户名@IP地址

修改root密码

mysqladmin -uroot -p 123456 password abcdef

数据库

DB操作：show databases;

添加DB：create database name;

删除DB：drop database name;

查看表结构：discribe + 表名称

显示集合：SELECT DISTINCT *column_name*,*column_name* FROM *table_name*;

distinct

|          |            |                  |                   |
| -------- | ---------- | ---------------- | ----------------- |
| 数据类型 | 大小(字节) | 用途             | 格式              |
| INT      | 4          | 整数             |                   |
| FLOAT    | 4          | 单精度浮点数     |                   |
| DOUBLE   | 8          | 双精度浮点数     |                   |
| ENUM     | --         | 单选,比如性别    | ENUM('a','b','c') |
| SET      | --         | 多选             | SET('1','2','3')  |
| DATE     | 3          | 日期             | YYYY-MM-DD        |
| TIME     | 3          | 时间点或持续时间 | HH:MM:SS          |
| YEAR     | 1          | 年份值           | YYYY              |
| CHAR     | 0~255      | 定长字符串       |                   |
| VARCHAR  | 0~255      | 变长字符串       |                   |
| TEXT     | 0~65535    | 长文本数据       |                   |

MySQL的约束：

| 约束类型： | 主键        | 默认值  | 唯一   | 外键        | 非空     |
| ---------- | ----------- | ------- | ------ | ----------- | -------- |
| 关键字：   | PRIMARY KEY | DEFAULT | UNIQUE | FOREIGN KEY | NOT NULL |

CREATE TABLE 表名（

id int(10)    **PRIMARY KEY**, //主键

name CHAR(20)

）

主键 (PRIMARY KEY)是用于约束表中的一行，作为这一行的唯一标识符，在一张表中通过主键就能准确定位到一行，因此主键十分重要，主键不能有重复记录且不能为空。

people_num INT(10) **DEFAULT 10,**

默认值约束 (DEFAULT) 规定，当有 DEFAULT 约束的列，插入数据为空时，将使用默认值。

唯一约束 (UNIQUE) 比较简单，它规定一张表中指定的一列的值必须不能有重复值，即这一列每个值都是唯一的。

外键 (FOREIGN KEY) 既能确保数据完整性，也能表现表之间的关系

一个表可以有多个外键，每个外键必须 REFERENCES (参考) 另一个表的主键，被外键约束的列，取值必须在它参考的列中有对应值

非空约束 (NOT NULL),听名字就能理解，被非空约束的列，在插入值时必须非空。

## 删除数据库

目前 Mysql 没有提供修改数据库名称的方法，因为这曾导致一系列安全问题。

在老版本中 RENAME DATABASE 可以修改数据库名称，这条命令在 MySQL 5.1.7 中被加入，但官方很快就发现这条命令所带来的危险，于是在 MySQL 5.1.23 中把这条命令移除。

#### 修改表名

RENAME TABLE 原名 TO 新名字;

ALTER TABLE 原名 RENAME 新名;

ALTER TABLE 原名 RENAME TO 新名;

#### 添加一列

ALTER TABLE 表名字 ADD COLUMN 列名字 数据类型 约束;

或： ALTER TABLE 表名字 ADD 列名字 数据类型 约束 （FIRST | AFTER xxx);

默认在最后

#### 删除一列

ALTER TABLE 表名字 DROP COLUMN 列名字;

或： ALTER TABLE 表名字 DROP 列名字;

#### 重命名一列

ALTER TABLE 表名字 CHANGE 原列名 新列名 数据类型 约束;

**注意：这条重命名语句后面的 “数据类型” 不能省略，否则重命名失败**

当**原列名**和**新列名**相同的时候，指定新的**数据类型**或**约束**，就可以用于修改数据类型或约束。需要注意的是，修改数据类型可能会导致数据丢失，所以要慎重使用。

ALTER TABLE 表名字 MODIFY 列名字 新数据类型;

#### 修改表中的某个值

UPDATE 表名字 SET 列1=值1,列2=值2 WHERE 条件;

#### 删除一行记录

DELETE FROM 表名字 WHERE 条件;

#### 查询数据

SELECT （* | 要查询的列名 ）FROM 表名字 WHERE 限制条件;

限制条件不止一个可以使用AND和OR进行判断

BETWEEN A AND B

关键词 **IN** 和 **NOT IN** 的作用和它们的名字一样明显，用于筛选**“在”**或**“不在”**某个范围内的结果

关键字 **LIKE** 可用于实现模糊查询，常见于搜索功能中。

和 LIKE 联用的通常还有通配符，代表未知字符。SQL中的通配符是 `_` 和 `%` 。其中 `_` 代表一个未指定字符，`%` 代表**不定个**未指定字符

#### 排序

为了使查询结果看起来更顺眼，我们可能需要对结果按某一列来排序，这就要用到 **ORDER BY** 排序关键词。默认情况下，**ORDER BY** 的结果是**升序**排列，而使用关键词 **ASC** 和 **DESC** 可指定**
升序**或**降序**排序。

SQL 允许对表中的数据进行计算。对此，SQL 有 5 个内置函数，这些函数都对 SELECT 的结果做操作：

| 函数名： | COUNT | SUM  | AVG      | MAX    | MIN    |
| -------- | ----- | ---- | -------- | ------ | ------ |
| 作用：   | 计数  | 求和 | 求平均值 | 最大值 | 最小值 |

其中 COUNT 函数可用于任何数据类型(因为它只是计数)，而 SUM 、AVG 函数都只能对数字类数据类型做计算，MAX 和 MIN 可用于数值、字符串或是日期时间数据类型。

SELECT MAX(salary) AS max_salary,MIN(salary) FROM employee;

**使用 AS 关键词可以给值重命名**，比如最大值被命名为了 max_salary：

### 分组查询

GROUP BY

#### 子查询

想要知道名为 "Tom" 的员工所在部门做了几个工程。员工信息储存在 employee 表中，但工程信息储存在 project 表中。

SELECT of_dpt,COUNT(proj_name) AS count_project FROM project GROUP BY of_dpt

HAVING of_dpt IN

(SELECT in_dpt FROM employee WHERE name='Tom');

#### 连接查询

SELECT id,name,people_num

FROM employee,department

WHERE employee.in_dpt = department.dpt_name

ORDER BY id;

SELECT id,name,people_num

FROM employee JOIN department

ON employee.in_dpt = department.dpt_name

ORDER BY id;

CONCAT(xxx,xxx) 连接操作

IFNULL(a,b)如果为NULL a->b

## 编码字符集问题

查看：

方法一：show variables like '%character%'; 方法二：show variables like 'collation%';

default-character-set=utf8

### 备份

导出：mysqldump -uroot -p123456 数据库名>地址

导入：mysql -uroot -p123456 数据库名<地址

导入：source 地址

## 外键

外键必须是另一个表的主键的值（外键要引用主键）

外键可以重复

外键可以为空

一张表可以有多个外键

