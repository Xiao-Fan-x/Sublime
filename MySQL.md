创建用户：create user 用户名@IP地址 identified  by '密码' //指定IP地址

修改密码：alter user '用户名'@'主机名' identified by '密码'	

create user 用户名@'%' IDENTIFIED BY '密码'

授予用户权限

grant 权限1,权限2,权限3... on 数据库.* to 用户名@IP地址

撤销用户权限：

revoke  权限1,权限2,权限3... ON 数据库.* FROM 用户名@IP地址

查看用户权限：

show grants for 用户名@IP地址

删除用户：

drop user 用户名@IP地址

修改root密码

mysqladmin -uroot -p 123456 password abcdef

数据库

DB操作：show databases;

添加DB：create database name;

删除DB：drop database name;

查看表结构：discribe + 表名称

显示集合：select distinct *column_name*,*column_name* FROM *table_name*;

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

create table 表名（

id int(10)    **PRIMARY KEY**, //主键

name char (20)

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
升序**或**降序\*\*排序。

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

删除/更新行为
no action / restrict 检查是否有对应外键，如果有则不允许删除/更新
cascade 检查是否有对应外键，如果有也删除/更新外键在子表的记录
set null 检查是否有对应外键，如果有则设置子集中改外键值为null（要求外键允许为null）
set default 父表有变更时，子表将外键列设置一个默认的值(Innodb不支持)




## 数值函数
ceil(x) 向上取整
floor(x) 向下取整
mod(x，y) 返回x/y的模
rdnd()	返回0\~1内的随机数
round(x,y) 求参数x的四舍五入的值，保留y位小数


## 隔离级别

Read Uncommitted(读取未提交内容) -- 脏读
Read Committed(读取提交内容) -- 大多数数据库系统的默认隔离级别
Repeatable Read(可重读) -- MySql的默认隔离级别
Serializable(可串行化) -- 


事务

开启commit rollback
set autocommit = 0;

开启一个事务
start transaction
commit



显示隔离级别
select @@transaction_isolation

设置事务隔离级别
set session transaction isolation level read uncommitted
set session transaction isolation level read committed
set session transaction isolation level repeatable read
set session transaction isolation level read serializable



savepoint 标识符为事务设置名称

使用rollback to 标识语句将事务回滚到指定的保存点而不中止事务



lock tables table_name [ read | write ]

冻结对数据库的所有写入操作

flush tables with read lock 







索引结构
B+Tree索引	最常见的索引类型，大部分引擎都支持B+树索引
Hash索引		底层数据结构是用哈希表实现的，只有精确匹配索引列的查询才有效，不支持范围查询
R-Tree(空间索引)		空间索引是MyISAM引擎的一个特殊索引类型，主要用于地理空间数据类型，通常使用较少
Full-Text(全文索引)	是一种通过建立倒排索引，快速匹配文档的方式，类似于Lucene、Solr、ES





| 索引      | InnoDB      | MyISAM | Memory |
| --------- | ----------- | ------ | ------ |
| B+Tree    | 支持        | 支持   | 支持   |
| Hash      | 不支持      | 不支持 | 支持   |
| R-Tree    | 不支持      | 支持   | 不支持 |
| Full-Text | 5.6版本之上 | 支持   | 不支持 |



索引分类



| 分类     | 含义                                                 | 特点                     | 关键字   |
| -------- | ---------------------------------------------------- | ------------------------ | -------- |
| 主键索引 | 针对于表中主键创建的索引                             | 默认自动创建，只能有一个 | primary  |
| 唯一索引 | 避免同一个表中某数据列中的值重复                     | 可以有多个               | unique   |
| 常规索引 | 快速定位特定数据                                     | 可以有多个               |          |
| 全文索引 | 全文索引查找的是文本中的关键词，而不是比较索引中的值 | 可以有多个               | fulltext |

索引分类

| 分类     | 含义                                                       |                      |
| -------- | ---------------------------------------------------------- | -------------------- |
| 聚集索引 | 将数据存储与索引放到一块，索引结构的叶子节点保存了行数据   | 必须有，而且只有一个 |
| 二级索引 | 将数据与索引分开储存，索引结构的叶子节点关联的是对应的主键 | 可以存在多个         |

如果存在主键，主键索引就是聚集索引

如果不存在主键，将使用第一个唯一索引作为聚集索引

如果没有主键，或没有适合的唯一索引，则InnoDB会自动生成一个rowid作为隐藏的聚集索引



创建索引

create [unique|fulltext] index index_name on table_name(index_col_name,...);

查看索引

show index from table_name;

删除索引

drop index index_name on table_name



## sql性能分析：

show session| global status like 'Com_______';

七个下划线如 Com_insert | update | delete



### 慢查询日志

记录了所有执行时间超过指定参数（long_query_time，单位：秒，默认10秒）的所有sql语句的日志

Mysql的妈妈查询日志默认没有开启，需要在MySQL的配置文件中配置信息：



 开启MySQL慢日志查询开关

slow_query_log=1

设置慢日志的时间为2秒，SQL语句执行时间超过2秒，就会视为慢查询，记录慢查询

long_query_time=2



show profiles 能够在做sql优化时帮助我们了解时间都耗费到哪里去了

通过have_profiling参数，能够看到当前，MySQL是否支持profile操作

select @@have_profiling;



select @@profiling;

set  [session|global] profiling = 1;

 

查看每一条sql的耗时基本情况

show profiles；

查看指定query_id的sql语句各个阶段的耗时情况

show profile for query_id;

查看指定query_id的sql语句cpu的使用情况

show profile cpu for query query_id;



### explain执行计划

 在select语句前加上关键字explain|desc

explain select * from 表名 where 条件;

- id:表操作的执行顺序，id相同，执行顺序从上到下，id不同，值越大，越先执行
- select_type:标识select类型，常见的取值有simple（简单表，即不适用表连接或者子查询）、primary（主查询，即外层的查询）、union（union中的第二个或者后面的查询语句）、subquery（select|where之后包含的子查询）等
- type:表示连接类型，性能由好到差的连接类型为null、system、const（唯一索引时出现）、eq_ref、ref（非唯一性索引）、range、index、all。
- possible_key：显示可能应用在这张表上的索引，一个或多个
- key：实际使用的索引，如果为null，则没有使用索引。
- key_len：表示索引中使用的字节数，该值为索引字段最大可能长度，并非实际使用长度，在不损失精确性的前提下，长度越短越好。
- rows：MySQL认为必须要执行的行数，在innodb引擎的表中，是一个估计值，可能并不总是准确的
- filtered：表示返回结果的行数占需要读取行数的百分比，filtered的值越大越好







## 索引使用

最左前缀法则











查看字符集

show character set

查看相关字符集的校对规则

SHOW COLLATION LIKE 'utf8%';



 命令查询当前服务器的字符集和校对规则

show variables like 'character_set_server';



二进制日志





























































































































## 一、数据库设计方面

1、对查询进行优化，应尽量避免全表扫描，首先应考虑在 `where` 及 `order by` 涉及的列上建立索引；

2、应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描，如： `select id from t where num is null` 可以在num上设置默认值0，确保表中num列没有null值，然后这样查询： `select id from t where num = 0`；

3、并不是所有索引对查询都有效，SQL是根据表中数据来进行查询优化的，**当索引列有大量数据重复时，查询可能不会去利用索引**，如一表中有字段sex，male、female几乎各一半，那么即使在sex上建了索引也对查询效率起不了作用；

4、索引并不是越多越好，索引固然可以提高相应的 `select` 的效率，但同时也降低了 `insert` 及 `update` 的效率，因为 `insert` 或 `update` 时有可能会重建索引，所以怎样建索引需要慎重考虑，视具体情况而定。**一个表的索引数最好不要超过6个**，若太多则应考虑一些不常使用到的列上建的索引是否有必要；

5、应尽可能的**避免更新索引数据列**，因为索引数据列的顺序就是表记录的物理存储顺序，一旦该列值改变将导致整个表记录的顺序的调整，会耗费相当大的资源。若应用系统需要频繁更新索引数据列，那么需要考虑是否应将该索引建为索引；

6、尽量使用数字型字段，若只含数值信息的字段尽量不要设计为字符型，这会降低查询和连接的性能，并会增加存储开销。这是因为引擎在处理查询和连接时会逐个比较字符串中每一个字符，而对于数字型而言只需要比较一次就够了；

7、尽可能的使用 `varchar/nvarchar` 代替 `char/nchar` ，因为首先变长字段存储空间小，可以节省存储空间，其次对于查询来说，在一个相对较小的字段内搜索效率显然要高些；

8、尽量使用表变量来代替临时表。如果表变量包含大量数据，请注意索引非常有限（只有主键索引）；

9、避免频繁创建和删除临时表，以减少系统表资源的消耗；

10、临时表并不是不可使用，适当地使用它们可以使某些例程更有效，例如，当需要重复引用大型表或常用表中的某个数据集时。但是，对于一次性事件，最好使用导出表;

11、在新建临时表时，如果一次性插入数据量很大，那么可以使用 `select into` 代替 `create table`，避免造成大量 log ，以提高速度；如果数据量不大，为了缓和系统表的资源，应先`create table`，然后`insert`；

12、如果使用到了临时表，在存储过程的最后务必将所有的临时表显式删除，先 `truncate table` ，然后 `drop table` ，这样可以避免系统表的较长时间锁定。

## 二、SQL语句方面

1、应尽量避免在 `where` 子句中使用`!=或<>`操作符，**否则将引擎放弃使用索引而进行全表扫描**；

2、应尽量避免在 `where` 子句中使用 `or` 来连接条件，**否则将导致引擎放弃使用索引而进行全表扫描**，如： `select id from t where num=10 or num=20` 可以这样查询： `select id from t where num=10 union all select id from t where num=20`;

3、`in` 和 `not in` 也要慎用，否则会导致全表扫描，如： `select id from t where num in(1,2,3)` 对于连续的数值，能用 `between` 就不要用 `in` 了： `select id from t where num between 1 and 3`；

4、下面的查询也将导致全表扫描： `select id from t where name like ‘%abc%’`

5、如果在 where 子句中使用参数，也会导致全表扫描。因为SQL只有在运行时才会解析局部变量，但优化程序不能将访问计划的选择推迟到运行时；它必须在编译时进行选择。然 而，如果在编译时建立访问计划，变量的值还是未知的，因而无法作为索引选择的输入项。如下面语句将进行全表扫描： `select id from t where num=@num` 可以改为强制查询使用索引： `select id from t with(index(索引名)) where num=@num`；

6、应尽量避免在 `where` 子句中对字段进行**表达式操作**，这将导致引擎放弃使用索引而进行全表扫描。如： `select id from t where num/2=100` 应改为: `select id from t where num=100*2`；

7、应尽量避免在`where`子句中对字段进行函数操作，这将导致引擎放弃使用索引而进行全表扫描。如： `select id from t where substring(name,1,3)=’abc’–name`以abc开头的id，`select id from t where datediff(day,createdate,’2005-11-30′)=0–‘2005-11-30’`生成的id 应改为: `select id from t where name like ‘abc%’ select id from t where createdate>=’2005-11-30′ and createdate<’2005-12-1′`

8、不要在 `where` 子句中的“=”左边进行函数、算术运算或其他表达式运算，否则系统将可能无法正确使用索引。

9、不要写一些没有意义的查询，如需要生成一个空表结构： `select col1,col2 into #t from t where 1=0` 这类代码不会返回任何结果集，但是会消耗系统资源的，应改成这样：` create table #t(…)`

10、很多时候用 `exists` 代替 `in` 是一个好的选择： `select num from a where num in(select num from b)` 用下面的语句替换： `select num from a where exists(select 1 from b where num=a.num)`

11、任何地方都不要使用 `select * from t` ，用具体的字段列表代替“\*”，不要返回用不到的任何字段。

12、尽量避免使用游标，因为游标的效率较差，如果游标操作的数据超过1万行，那么就应该考虑改写。


13、尽量避免向客户端返回大数据量，若数据量过大，应该考虑相应需求是否合理。

14、尽量避免大事务操作，提高系统并发能力。

## 三、Java方面

1、尽可能的少造对象；

2、合理摆正系统设计的位置。大量数据操作，和少量数据操作一定是分开的。大量的数据操作，肯定不是ORM框架搞定的；

3、使用JDBC连接数据库操作数据；

4、控制好内存，让数据流起来，而不是全部读到内存再处理，而是边读取边处理；

5、合理利用内存，有的数据要缓存；

## 四、如何优化数据库，如何提高数据库的性能?

1、硬件调整性能

最有可能影响性能的是磁盘和网络吞吐量,解决办法扩大虚拟内存，并保证有足够可以扩充的空间；把数据库服务器上的不必要服务关闭掉；把数据库服务器和主域服务器分开；把SQL数据库服务器的吞吐量调为最大；在具有一个以上处理器的机器上运行SQL。

2、调整数据库

若对该表的查询频率比较高，则建立索引；建立索引时，想尽对该表的所有查询搜索操作， 按照where选择条件建立索引，尽量为整型键建立为有且只有一个簇集索引，数据在物理上按顺序在数据页上，缩短查找范围，为在查询经常使用的全部列建立 非簇集索引，能最大地覆盖查询；但是索引不可太多，执行UPDATE DELETE INSERT语句需要用于维护这些索引的开销量急剧增加；避免在索引中有太多的索引键；避免使用大型数据类型的列为索引；保证每个索引键值有少数行。

3、使用存储过程（注意：阿里巴巴开发规范中已经明确禁止使用存储过程了，这里只是列出，不作为优化方法！）

应用程序的实现过程中，能够采用存储过程实现的对数据库的操作尽量通过存储过程来实现，因为存储过程是存放在数据库服务器上的一次性被设计、编码、 测试，并被再次使用，需要执行该任务的应用可以简单地执行存储过程，并且只返回结果集或者数值，这样不仅可以使程序模块化，同时提高响应速度，减少网络流 量，并且通过输入参数接受输入，使得在应用中完成逻辑的一致性实现。

4、应用程序结构和算法

建立查询条件索引仅仅是提高速度的前提条件，响应速度的提高还依赖于对索引的使用。因为人们在使用SQL时往往会陷入一个误区，即太关注于所得的结 果是否正确，特别是对数据量不是特别大的数据库操作时，是否建立索引和使用索引的好坏对程序的响应速度并不大，因此程序员在书写程序时就忽略了不同的实现 方法之间可能存在的性能差异，这种性能差异在数据量特别大时或者大型的或是复杂的数据库环境中（如联机事务处理OLTP或决策支持系统DSS）中表现得尤 为明显。在工作实践中发现，不良的SQL往往来自于不恰当的索引设计、不充份的连接条件和不可优化的where子句。在对它们进行适当的优化后，其运行速 度有了明显地提高！
