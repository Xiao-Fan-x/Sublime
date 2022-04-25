构造函数实例化如果有static属性

public class TestServiceImpl{

​	public static class Aa{

​	}

}

<bean id=" " class="com.java,service,TestServiceImpl$Aa"> </bean>

使用$字符将嵌套的类名与外部类名分开



Bean实例化的三种方式

- 构造器实例化

<bean id = "goodsService" class="">

- 静态工厂实例化

  class：静态工厂类路径

  factory-method：静态方法名

- 实例化工厂

  1.将实例化工厂以bean对象的形式交给ioc容器

  2.配置bean对象

  id：orderService

  factory-bean：引用实例化工厂id

  factory-method：返回对象的方法名称

  ```
  <bean id="instanceFactory" class="com.spring.Factory.InstanceFactory"></bean>
  
  <bean id="orderService" factory-bean="instanceFactory" factory-method="createOrderService"></bean>
  ```
  
  

属性注入

<property name="" ref=""|value="" ></property>

集合注入

```
<property name="">
<list><>value></value></list>
<set><>value></value></set>
<map><entry key="" value=""></map>
</property>
```

properties 类

<property name= "propertoes">

​	<props>

​		<prop key="">\*\*\*</prop>

​		<prop key="">\*\*\*</prop>

​		<prop key="">\*\*\*</prop>

​	</props>

<property>

P标签：xmlns:p="http://www.springframework.org/schema/p" （用与set.get方法）

C标签：xmlns:c="http://www.springframework.org/schema/c" (用于构造方法) 





```
xmlns:context="http://www.springframework.org/schema/context"

http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
```



```
@Autowired
@Qualifier(value = "")
```



inject

<!-- https://mvnrepository.com/artifact/javax.inject/javax.inject -->
<dependency>
    <groupId>javax.inject</groupId>
    <artifactId>javax.inject</artifactId>
    <version>1</version>
</dependency>



邮件api

<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-mail -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
    <version>2.3.12.RELEASE</version>
</dependency>


事务控制
Spring 事务管理接口
TransactionDefinition

PlatformTransactionManger   DataSourceTransactionManger   JDBC
                            HibernateTransactionManger    Hibernate
                            JpaTransactionManger          JPA
                            JtaTransactionManger          JTA


编程式
声明式

aop代理
<aop:aspectj-autoproxy/>

配置事务传播特性
tx:advice





@RestControllerAdvice



@ExceptionHandler

