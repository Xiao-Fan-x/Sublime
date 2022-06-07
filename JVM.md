-Xss 栈空间

Linux环境下查看 JVM

top 

ps H -eo pid,tid,%cpu | grep 进程id （用ps命令进一步定位是哪个线程引起的cpu占用过高）

jstack 进程id



-Xmx 堆内存

jps：查看系统中的Java进程

jmap：查看堆内存占用情况  cmd :  jmap  -heap  进程id

jconsole：图形界面，多功能的监测工具，可以连续监测

jvisualvm：强力的监测工具 



-XX:MaxMetaspaceSize=8m  元空间大小

元空间内存溢出：java .lang.OutOfMemoryError: Metaspace

-XX:MaxPermSize=8m 	永久代内存大小

永久代内存溢出：java.lang.OutOfMemoryError: PermGen space



反编译

javap -v  *.class 



StringTable 垃圾回收

-Xmx10m  -XX:+PrintStringTableStatistics  -XX:+PrintGCDetails -verbose:gc



常量池HashTable的桶大小

-XX:StringTableSize=



操作系统内存  Unsafe类

```java
分配系统内存 ：   
unsafe.allocateMemory();
unsafe.setMemory();

释放内存
unsafe.freeMemory();
```



-XX:+DisableExplicitGC   禁用显示的垃圾回收（程序员无法直接操作 system.gc()无效）



## 垃圾回收

引用计数

jmap -dump:format=b,live,file=1.bin 进程id



强引用

软引用

弱引用

虚引用

终结器引用



