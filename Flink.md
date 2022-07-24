流处理基准测试

Nexmark



![image-20220628165312985](C:\Users\17430\Documents\github\Sublime\新建文件夹\image-20220628165312985.png)

在大数据场景下经常需要数据同步或者数据集成，也就是将数据库中的
数据同步到大数据的数仓或者其他存储中。上图中的左边是传统的经典数据集成的模式之
一，全量的同步和增量的同步实际上是两套技术，我们需要定期将全量同步的数据跟增量
同步数据做 merge ，不断的迭代来把数据库的数据同步到数据仓库中。但基于 Flink 流批一体
的话，整个数据集成的架构将截然不同。因为 FlinkSQL 也支持数据库（像 MySQL 和 PG ）的
CDC 语义，所以可以用 FlinkSQL 一键同步数据库的数据到 Hive、ClickHouse、TiDB
等开源的数据库或开源的 KV 存储中。在 Flink 流批一体架构的基础上，Flink 的 connector
也是流批混合的，它可以先读取数据库全量数据同步到数仓中，然后自动切换到增量模式，
通过 CDC 读 Binlog 进行增量和全量的同步，Flink 内部都可以自动的去协调好，这就是
流批一体的价值。





## docker 开启 flink 

```cmd
FLINK_PROPERTIES="jobmanager.rpc.address: jobmanager"
docker network create flink-network


docker run --rm --name=jobmanager --network flink-network --publish 8081:8081 --env FLINK_PROPERTIES="jobmanager.rpc.address: jobmanager" flink:1.13.6-scala_2.12-java8 jobmanager

docker run --rm --name=taskmanager --network flink-network --env FLINK_PROPERTIES="jobmanager.rpc.address: jobmanager" flink:1.13.6-scala_2.12-java8 taskmanager

```



Flink开启模式（流|批）

```
批处理
1.命令行
bin/flink run -Dexecution.runtime-mode=BATCH ...
2.代码
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
env.setRuntimeMode(RuntimeExecutionMode.BATCH);

```

```Java
Flink Stream 分区

1.随机分区
stream.shuffle()

2.轮询分区
stream.rebalance()

3.rescale重缩放分区
stream.rescale()

4.广播分区（将每条数据发送到所有分区）
stream.global()

5.全局分区（将所有分区合并到第一个）

```
