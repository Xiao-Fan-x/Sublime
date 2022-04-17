显示系统环境
mvn help : system

Maven 项目文档
mvn site

定义环境 
```java

<profiles>
<profile>
<id></id>

设置默认启动
<actication>
<activeByDefault>true</activeByDefault>
</actication>

</profile>
</profiles>

mvn install -P + profile.id
```

idea配置
```
<distributionManagement>
	<repository>
	<id>
	<url>
	
	</repository>
	
	<snapshotRepository>
	</snapshotRepository>
</distributionManagement>
```



mvn dependency:list

mvn dependency:tree

