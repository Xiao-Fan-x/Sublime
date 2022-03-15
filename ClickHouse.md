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


