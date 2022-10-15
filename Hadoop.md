Hadoop 3.2.4



一、安装

解压下载的 Hadoop 发行版。

在发行版中，编辑文件`/hadoop/hadoop-env.sh`以定义一些参数

```
  # 设置为 Java 安装的根目录
  export JAVA_HOME=/usr/java/latest
```



hadoop 运行模式

1.独立操作 （默认） 单个java进程，用于调试

2.伪分布式操作 

Hadoop 也可以在单节点上以伪分布式模式运行，其中每个 Hadoop 守护进程在单独的 Java 进程中运行。

$HADOOP_HOME/etc/hadoop/core-site.xml:

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <!-- 指定 NameNode 的地址 --> 
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://hadoop102:8020</value> 
  	</property>
    <!-- 指定 hadoop 数据的存储目录 -->
    <property>
   	 		<name>hadoop.tmp.dir</name> 
      	<value>/opt/module/hadoop-3.2.4/data</value>
    </property>
		<!-- 配置 HDFS 网页登录使用的静态用户为 atguigu --> 
    <property>
        <name>hadoop.http.staticuser.user</name>
        <value>staryea</value> 
    </property>
</configuration>
```

$HADOOP_HOME/etc/hadoop/hdfs-site.xml:

```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
<configuration>
    <!-- nn web端访问地址--> 
    <property>
        <name>dfs.namenode.http-address</name>
        <value>hadoop102:9870</value> 
    </property>
    <!-- 2nn web 端访问地址--> 
    <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>hadoop104:9868</value> 
    </property>
</configuration>
```

vim yarn-site.xml

```xml
<configuration>
<!-- 指定 MR 走 shuffle --> 
  	<property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value> 
    </property>
<!-- 指定 ResourceManager 的地址--> 
  	<property>
        <name>yarn.resourcemanager.hostname</name>
        <value>hadoop103</value> 
    </property>
		<!-- 环境变量的继承 -->
  	<property> 
    		<name>yarn.nodemanager.env-whitelist</name>
  <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAP RED_HOME</value>
       </property>
</configuration>
```

MapReduce 配置文件

配置 mapred-site.xml

```xml
<configuration>
<!-- 指定 MapReduce 程序运行在 Yarn 上 --> <property>
<name>mapreduce.framework.name</name>
       <value>yarn</value>
   </property>
</configuration>	
```

配置 **workers**

vim hadoop- 3.1.3/etc/hadoop/workers

```
hadoop102
hadoop103
hadoop104
```



## 启动集群：

格式化 NameNode，会产生新的集群 id，导致 NameNode 和 DataNode 的集群 id 不一致，集群找 不到已往数据。如果集群在运行过程中报错，需要重新格式化 NameNode 的话，一定要先停 止 namenode 和 datanode 进程，并且要删除所有机器的 data 和 logs 目录，然后再进行格式化。







