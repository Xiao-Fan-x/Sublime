SpringBoot 4级配置文件

1.file : config/application.yml

2.file : application.yml

3.classpath : config/application.yml

3.classpath : application.yml



自定义文件名

--spring.config.name=config_name

自定义路径

--spring.config.location:classpath:/config_name



多环境开发：

spring.profiles,active=

spring.profiles.include=   (include=active+name)

spring.profiles.group=

application.yml

application-dev.yml

application-test.yml





## maven与springboot多环境兼容

```xml
pom.xml中
<profiles>
	<profile>
    	<id>dev</id>
        <properties>
        	<profile.active>dev</profile.active>
        </properties>
        <activation>
        	<activeByDefault>true</activeByDefault>
        </activation>
    </profile>
</profiles>

application.tml中 
spring:
	profiles:
		active: @profile.active@
```



热部署 springboot devtools

```xml
devtools:
	restart:
		exclude: static/**,public/**,config/application.yml
		//设置热部署排除地址
```



```
为第三方Bean绑定属性
@ConfigurationProperties
```



