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

  <bean id="instanceFactory" class="com.spring.Factory.InstanceFactory"></bean>

  <bean id="orderService" factory-bean="instanceFactory" factory-method="createOrderService"></bean>



property 类

<property name= "propertoes">

​	<props>

​		<prop key="">***</prop>

​		<prop key="">***</prop>

​		<prop key="">***</prop>

​	</props>

<property>

