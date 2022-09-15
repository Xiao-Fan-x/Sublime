流处理基准测试

Nexmark

![image-20220628165312985](Flink.assets/image-20220628165312985.png)

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



```shell
Flink start|kill

bin/start-cluster.sh
bin/stop-cluster.sh

Master-slave 主从
节点添加：
vim flink-conf.yaml
# JobManager 节点地址. 
jobmanager.rpc.address: hadoop102

vim workers
hadoop103
hadoop104

优化：
- jobmanager.memory.process.size:对JobManager进程可使用到的全部内存进行配置，
包括 JVM 元空间和其他开销，默认为 1600M，可以根据集群规模进行适当调整。
- taskmanager.memory.process.size:对TaskManager进程可使用到的全部内存进行配置，
包括 JVM 元空间和其他开销，默认为 1600M，可以根据集群规模进行适当调整。
- taskmanager.numberOfTaskSlots:对每个TaskManager能够分配的Slot数量进行配置，
默认为 1，可根据 TaskManager 所在的机器能够提供给 Flink 的 CPU 数量决定。所谓
Slot 就是 TaskManager 中具体运行一个任务所分配的计算资源。
- parallelism.default:Flink任务执行的默认并行度，优先级低于代码中进行的并行度配
置和任务提交时使用参数指定的并行度数量。
```



```xml
pom.xml 打包
<build>
	<plugins>
		<plugin>
    	<groupId>org.apache.maven.plugins</groupId>
    	<artifactId>maven-assembly-plugin</artifactId>
     	<version>3.0.0</version>
     	<configuration>
				<descriptorRefs>
        	<descriptorRef>jar-with-dependencies</descriptorRef>
   			</descriptorRefs>
			</configuration>
			<executions>
   			<execution>
       		<id>make-assembly</id>
       		<phase>package</phase>
       		<goals>
          	<goal>single</goal>
            </goals>
         	</execution>
    		</executions>
  	</plugin>
	</plugins>
</build>
```



```shel
Flink 集群
bin/flink run -m (指定JobManager) -c (程序入口类)  xxx.jar
```





## 部署模式：

1.会话模式

2.单作业模式

3.应用模式



### 会话模式：

先启动集群再提交作业

会话模式比较适合于单个规模小、执行时间短的大量作业。

缺点明显：因为资源是共享的，所以资源不够了，提交新的 作业就会失败。另外，同一个 TaskManager 上可能运行了很多作业，如果其中一个发生故障导 致 TaskManager 宕机，那么所有作业都会受到影响。



## 单作业模式

为每个提交的作业启动一个集群



## 应用模式

不要客户端，直接把应用提交到 JobManger 上运行

需要为每一个提交的应用单独启动一个 JobManager，也就是创建一个集群



应用模式与单作业模式，都是提交作业之后才创建集群；

单作业模式是通过客户端来提交的，客户端解析出的每一个作业对应一个集群；

而应用模式下，是直接由 JobManager执行应用程序的，并且即使应用包含了多个作业，也只创建一个集群。



## 高可用

JobManager（主-备）

```she
## flink-conf.yaml文件：
high-availability: zookeeper
high-availability.storageDir: hdfs://hadoop102:9820/flink/standalone/ha
high-availability.zookeeper.quorum:
hadoop102:2181,hadoop103:2181,hadoop104:2181
high-availability.zookeeper.path.root: /flink-standalone
high-availability.cluster-id: /cluster_atguigu

masters:
hadoop102:8081
hadoop103:8081
```

TaskManager（多节点- 重启）





## Yarn模式

YARN 上部署的过程是：

客户端把 Flink 应用提交给 Yarn 的 ResourceManager，Yarn 的 ResourceManager 会向 Yarn 的 NodeManager 申请容器。在这些容器上，Flink 会部署 JobManager 和 TaskManager 的实例，从而启动集群。Flink 会根据运行在 JobManger 上的作业 所需要的 Slot 数量动态分配 TaskManager 资源

