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