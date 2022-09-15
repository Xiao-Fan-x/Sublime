分区表
早在 10 版本之前 PostgreSQL 分区表一般通过继承加触发器方式实现，称为传统分区表。

PostgreSQL 10 版本提供的分区表称为内置分区表。

传统分区表
传统分区表是通过继承和触发器方式实现的， 其实现过程步骤多， 非常复杂，需要定义父表、定义子表、 定义子表约束 、 创建子表索引 、 创建分区插入、 删除 、 修改函数和触发器等， 可以说是在普通表基础上手工实现的分区表。继承是传统分区表的重要组成部分。

继承表
首先定义一张父表，然后创建子表并继承父表

示例
创建一张日志模型表 tbl_log

create table tbl_log(id int4, create_date date, log_type text);

创建一张子表tbl_log_sql用于存储 SQL 日志

create table tbl_log_sql(sql text) INHERITS(tbl_log);
-- 通过INHERITS(tbl_log)关键字表示tbl_log_sql继承表tbl_log，子表可以定义额外的字段


查看表结构
\d tbl_log_sql

DML操作
父表和子表分别插入记录

INSERT INTO tbl_log VALUES (1,'2021-10-10', null);
INSERT INTO tbl_log_sql VALUES (2,'2021-10-10', null,'select 1;');

select * from tbl_log; -- 查询父表 tbl_log 会显示两条的记录，但子表的字段不会显示
select * from tbl_log_sql;

若只查询父表记录，需要在父表名称前加上ONLY关键字
select * from only tbl_log;

注意：对于使用了继承表的场景，对父表的update, delete的操作需谨慎，它会对父表和子表的数据进行DML操作


创建分区表
步骤
1.创建父表
2.通过 INHERITS 方式创建继承表，也称之为子表或分区
3.给子表创建约束
4.给子表创建索引，继承操作不会继承父表上的索引
5.在父表上定义 INSERT 、 DELETE 、 UPDATE 触发器，将 SQL 分发到对应分区（可选）
6.启用 constraint_exclusion 参数

具体实现
创建一张范围分区表，并且定义年月子表存储月数据

CREATE TABLE log_ins (id serial,
user_id int4,
create_time timestamp(O) without time zone);

创建子表

CREATE TABLE log_ins_history(CHECK ( create_time < '2021-01-01')) INHERITS (log_ins);
CREATE TABLE log_ins_202101(CHECK ( create_time >= '2021-01-01' and create_time < '2021-02-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202102(CHECK ( create_time >= '2021-02-01' and create_time < '2021-03-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202103(CHECK ( create_time >= '2021-03-01' and create_time < '2021-04-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202104(CHECK ( create_time >= '2021-04-01' and create_time < '2021-05-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202105(CHECK ( create_time >= '2021-05-01' and create_time < '2021-06-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202106(CHECK ( create_time >= '2021-06-01' and create_time < '2021-07-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202107(CHECK ( create_time >= '2021-07-01' and create_time < '2021-08-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202108(CHECK ( create_time >= '2021-08-01' and create_time < '2021-09-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202109(CHECK ( create_time >= '2021-09-01' and create_time < '2021-10-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202110(CHECK ( create_time >= '2021-10-01' and create_time < '2021-11-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202111(CHECK ( create_time >= '2021-11-01' and create_time < '2021-12-01')) INHERITS(log_ins);
CREATE TABLE log_ins_202112(CHECK ( create_time >= '2021-12-01' and create_time < '2022-01-01')) INHERITS(log_ins);


创建子表索引

CREATE INDEX idx_his_ctime ON log_ins_history USING btree (create_time);
CREATE INDEX idx_log_his_202101_ctime ON log_ins_202101 USING btree (create_time);
CREATE INDEX idx_log_his_202102_ctime ON log_ins_202102 USING btree (create_time);
CREATE INDEX idx_log_his_202103_ctime ON log_ins_202103 USING btree (create_time);
CREATE INDEX idx_log_his_202104_ctime ON log_ins_202104 USING btree (create_time);
CREATE INDEX idx_log_his_202105_ctime ON log_ins_202105 USING btree (create_time);
CREATE INDEX idx_log_his_202106_ctime ON log_ins_202106 USING btree (create_time);
CREATE INDEX idx_log_his_202107_ctime ON log_ins_202107 USING btree (create_time);
CREATE INDEX idx_log_his_202108_ctime ON log_ins_202108 USING btree (create_time);
CREATE INDEX idx_log_his_202109_ctime ON log_ins_202109 USING btree (create_time);
CREATE INDEX idx_log_his_202110_ctime ON log_ins_202110 USING btree (create_time);
CREATE INDEX idx_log_his_202111_ctime ON log_ins_202111 USING btree (create_time);
CREATE INDEX idx_log_his_202112_ctime ON log_ins_202112 USING btree (create_time);


-- 创建触发器函数，设置数据插入父表时的路由规则
create or replace function log_hit_insert_trigger()
 returns trigger
 language plpgsql
as $function$
begin
 if (NEW.create_time < '2021-01-01') then
  insert into log_ins_history values (NEW.*);
 elsif (NEW.create_time >= '2021-01-01' and NEW.create_time < '2021-02-01') then
  insert into log_ins_202101 values (NEW.*);
 elsif (NEW.create_time >= '2021-02-01' and NEW.create_time < '2021-03-01') then
  insert into log_ins_202102 values (NEW.*);
 elsif (NEW.create_time >= '2021-03-01' and NEW.create_time < '2021-04-01') then
  insert into log_ins_202103 values (NEW.*);
 elsif (NEW.create_time >= '2021-04-01' and NEW.create_time < '2021-05-01') then
  insert into log_ins_202104 values (NEW.*);
 elsif (NEW.create_time >= '2021-05-01' and NEW.create_time < '2021-06-01') then
  insert into log_ins_202105 values (NEW.*);
 elsif (NEW.create_time >= '2021-06-01' and NEW.create_time < '2021-07-01') then
  insert into log_ins_202106 values (NEW.*);
 elsif (NEW.create_time >= '2021-07-01' and NEW.create_time < '2021-08-01') then
  insert into log_ins_202107 values (NEW.*);
 elsif (NEW.create_time >= '2021-08-01' and NEW.create_time < '2021-09-01') then
  insert into log_ins_202108 values (NEW.*);
 elsif (NEW.create_time >= '2021-09-01' and NEW.create_time < '2021-10-01') then
  insert into log_ins_202109 values (NEW.*);
 elsif (NEW.create_time >= '2021-10-01' and NEW.create_time < '2021-11-01') then
  insert into log_ins_202110 values (NEW.*);
 elsif (NEW.create_time >= '2021-11-01' and NEW.create_time < '2021-12-01') then
  insert into log_ins_202111 values (NEW.*);
 elsif (NEW.create_time >= '2021-12-01' and NEW.create_time < '2022-01-01') then
  insert into log_ins_202112 values (NEW.*);
 else
  raise exception 'create_time out of range.';
 end if;
 return NULL;
END;
$function$;

-- 创建触发器
CREATE TRIGGER insert_log_ins_trigger BEFORE INSERT ON log_ins FOR EACH ROW
EXECUTE PROCEDURE log_hit_insert_trigger();

使用分区表
插入数据

INSERT INTO log_ins(user_id,create_time)
SELECT round(100000000*random()),generate_series('2020-12-01'::date,
'2021-12-01'::date , '1 minute');

SELECT count(*) FROM log_ins;
SELECT count(*) FROM ONLY log_ins;

SELECT * FROM ONLY log_ins limit 2;

SELECT min(create_time),max(create_time) FROM log_ins_202101;

-- 会话级别设置参数
set constraint_exclusion = off;
EXPLAIN ANALYZE SELECT * FROM log_ins_202101 WHERE create_time > '2021-01-01' AND create time < '2021-02-01';

添加分区
创建分区
CREATE TABLE log_ins_202201(LIKE log_ins INCLUDING ALL);

添加约束
ALTER TABLE log_ins_202201 ADD CONSTRAINT log_ins_202201_create_time check
CHECK ( create_time >= '2022-01-01' AND create_time < '2022-02-01');

新分区 log_ins_202101 继承到父表 log_ins

ALTER TABLE log_ins_202201 INHERIT log_ins;

删除分区
\1. 直接删除分区方式
DROP TABLE log_ins_202201;

\2. 先将分区的继承关系去掉后删除
ALTER TABLE log_ins_202201 NO INHERIT log_ins;
DROP TABLE log_ins_202201;


查看分区信息

SELECT
 nmsp_parent.nspname as parent_schema,
 parent.relname as parent,
 nmsp_child.nspname as child_schema,
 child.relname as child
from
 pg_inherits join pg_class parent on pg_inherits.inhparent = parent.oid 
 join pg_class child on pg_inherits.inhrelid = child.oid 
 join pg_namespace nmsp_parent on nmsp_parent.oid = parent.relnamespace 
 join pg_namespace nmsp_child on nmsp_clild.oid = child.relnamespace
where parent.relname = 'log_ins';

-- 分区表的分区数量

select 
 nspname,
 relname,
 count(*) as partition_num
from
 pg_class c,
 pg_namespace n,
 pg_inherits i
where c.oid = i.inhparent
 and c.relnamespace = n.oid
 and c.relhassubclass
 and c.relkind in ('r','p')
group by 1,2 
order by partition_num desc;


内置分区表
PostgreSQL10 一个重量级新特性是支持内置分区表，用户不需要预先在父表上定义INSERT 、 DELETE 、 UPDATE 触发器，对父表的 DML 操作会自动路由到相应分区，相比传统分区表大幅度降低了维护成本，PostgreSQL10目前仅支持范围分区和列表分区。

内置分区表实际与传统分区表一样，都是用继承的方式实现。


创建内置分区表步骤
创建父表，指定分区键和分区策略 。
创建分区，创建分区时须指定分区表的父表和分区键的取值范围，注意分区键的范围不要有重叠，否则会报错 。
在分区上创建相应索引，通常情况下分区键上的索引 是必须的，非分区键的索引可根据实际应用场景选择是否创建 。

示例
创建内置分区表过程

-- 1. 创建范围分区表
CREATE TABLE log_par (
    id serial,
  user_id int4,
  create_time timestamp(0) without time zone
) PARTITION BY RANGE(create_time);

-- 2. 创建分区
create table log_par_his partition of log_par for values from ('1970-01-01') to ('2020-01-01');
create table log_par_202001 partition of log_par for values from ('2020-01-01') to ('2020-02-01');
create table log_par_202002 partition of log_par for values from ('2020-02-01') to ('2020-03-01');

-- 3. 创建分区索引
create index idx_log_par_his_ctime on log_par_his using btree(create_time);
create index idx_log_par_202001_ctime on log_par_202001 using btree(create_time);
create index idx_log_par_202002_ctime on log_par_202002 using btree(create_time);


使用分区
-- 1. 插入数据
insert into log_par(user_id, create_time)
select round(1000000*random()), generate_series('2019-12-01'::date, '2020-02-28'::date, '1 minute');

-- 2. 查看数据
select count(*) from log_par;
select count(*) from only log_par;

内置分区表与其分区的继承关系

select 
  nmsp_parent.nspname as parent_schema, 
  parent.relname as parent,
  nmsp_child.nspname as child_schema,
  child.relname as child_schema
from pg_inherits join pg_class parent
  on pg_inherits.inhparent = parent.oid join pg_class child
  on pg_inherits.inhrelid = child.oid join pg_namespace nmsp_parent
  on nmsp_parent.oid = parent.relnamespace join pg_namespace nmsp_child
  on nmsp_child.oid = child.relnamespace
where 
  parent.relname = 'log_par';



添加分区
CREATE TABLE log_par_202101 PARTITION OF log_par FOR VALUES FROM ('2021-01-01') TO ('2021-02-01');
创建索引
CREATE INDEX idx_log_par_202101_ctime ON log_par_202101 USING btree(create_time);


删除分区
\1. 直接删分区方式
DROP TABLE log_par_202101;
\2. 解绑分区方式
-- 解绑分区,分区和数据仍然保留
ALTER TABLE log_par DETACH PARTITION log_par_202101;

-- 恢复分区
ALTER TABLE log_par ATTACH PARTITION log_par_202101 FOR VALUES FROM ('2021-01-01') TO ('2021-02-01');