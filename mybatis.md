对于像Oracle这样的数据，没有提供主键自增的功能，而是使用序列的方式获取自增主键。
可以使用＜selectKey＞标签来获取主键的值，这种方式不仅适用于不提供主键自增功能的数据库，也适用于提供主键自增功能的数据库
＜selectKey＞一般的用法

```
<selectKey keyColumn="id" resultType="long" keyProperty="id" order="BEFORE">
</selectKey> 
```
keyProperty	selectKey 语句结果应该被设置的目标属性。如果希望得到多个生成的列，也可以是逗号分隔的属性名称列表。
keyColumn	匹配属性的返回结果集中的列名称。如果希望得到多个生成的列，也可以是逗号分隔的属性名称列表。
resultType	结果的类型，MyBatis 通常可以推算出来。MyBatis 允许任何简单类型用作主键的类型，包括字符串。如果希望作用于多个生成的列，则可以使用一个包含期望属性的 Object 或一个 Map。
order	值可为BEFORE 或 AFTER。如果是 BEFORE，那么它会先执行selectKey设置 keyProperty 然后执行插入语句。如果为AFTER则相反。
statementType	使用何种语句类型，默认PREPARED。 有STATEMENT，PREPARED 和 CALLABLE 语句的映射类型。



```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <environments default="product">
        <environment id="product">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">

            </dataSource>
        </environment>
    </environments>

</configuration>
```



延迟加载

fetchType="lazy | eager"

association  实体类  属性

collection  ofType 集合中属性的类型



一级缓存 -> sqlSession级别

失效的四种情况：

1.不同的SqlSession对应不同的一级缓存

2.同一个SqlSession但是查询条件不同

3.同一个SqlSession两次查询期间执行了任何一次增删改操作

4.同一个SqlSession两次查询期间手动清空了缓存



二级缓存 -> SqlSessionFactory级别

开启： a> cacheEnabled="true"

​			b> <cache />

​			c> 二级缓存必须在SQL Session关闭或提交之后有效

​			d> 查询的数据所转换的实体类类型必须实现序列化接口



ehcache 第三方缓存









