SIMD指令
ClickHouse目前利用SSE4.2指令集实现向量化执行

clickhouse 吃cpu，linux对此有限制，需要修改
ulimit -a
open files    文件数
max user processes  用户最大线程

sudo vim /etc/security/limits.conf

\* soft nofile 65536
\* hard nofile 65536
\* soft nproc 131072
\* hard nproc 131072

sudo vim /etc/security/limits.d/20-nproc.conf


optimize table table_name final; 手动合并临时分区
可以在final前增加partition ‘分区名’  对指定分区进行合并


二级索引
INDEX a total amount TYPE minmax GRANULARITY 5

TTL Time To Live, MergeTree 提供了可以管理数据表或者列的生命周期的功能
过期的数据会 


ReplacingMergeTree 合并去重，不夸分区  保证最终的一致性 ，不能保证不存在重复
使用ORDER BY排序键，作为判断数据是否重复的唯一键
只有在合并分区时，才会触发数据的去重逻辑
删除重复数据，是以数据分区为单位。同一个数据分区的重复数据才会被删除，不同数据分区的重复数据仍会保留
在进行数据去重时，由于已经基于ORDER BY排序，所以可以找到相邻的重复数据
数据去重策略为：
若指定了ver参数，则会保留重复数据中，ver字段最大的那一行
若未指定ver参数，则会保留重复数据中最末的那一行数据


Update 和 Delete
Mutation查询 可变查询 ，可以看作Alter 的一种
这是一种很重的操作，而且不支持事务
操作会导致放弃目标数据的原有分区，重建新分区，尽量做批处理的更改，不进行频繁的小数据操作

alter table table_name delete where ...;
alter table table_name update  ...  where ... ;


多维分析
group by  a,b,c  with rollup| with cube | with total
rollup ：上卷
cube：
total：
```
BY year, month, day WITH CUBE;
-   `GROUP BY year, month, day`
-   `GROUP BY year, month`
-   `GROUP BY year, day`
-   `GROUP BY year`
-   `GROUP BY month, day`
-   `GROUP BY month`
-   `GROUP BY day`
-   and totals.



GROUP BY year, month, day WITH ROLLUP;
-   `GROUP BY year, month, day`;
-   `GROUP BY year, month`（并且列用零填充）;`day`
-   `GROUP BY year`（现在列都用零填充）;`month, day`
-   and totals.（所有三个关键表达式列均为零）。

GROUP BY year, month, day WITH total;
只显示总计


```