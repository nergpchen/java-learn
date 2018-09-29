### SqlSessionTemplate

SqlSessionTemplate 是 MyBatis-Spring 的核心。 这个类负责管理 MyBatis 的 SqlSession, 调用 MyBatis 的 SQL 方法, 翻译异常。 SqlSessionTemplate 是线程安全的, 可以被多个 DAO 所共享使用。

当调用 SQL 方法时, 包含从映射器 getMapper\(\)方法返回的方法, SqlSessionTemplate 将会保证使用的 SqlSession 是和当前 Spring 的事务相关的。此外,它管理 session 的生命 周期,包含必要的关闭,提交或回滚操作。

SqlSessionTemplate 实现了 SqlSession 接口,这就是说,在代码中无需对 MyBatis 的 SqlSession 进行替换。 SqlSessionTemplate 通常是被用来替代默认的 MyBatis 实现的 DefaultSqlSession , 因为模板可以参与到 Spring 的事务中并且被多个注入的映射器类所使 用时也是线程安全的。相同应用程序中两个类之间的转换可能会引起数据一致性的问题。

SqlSessionTemplate 对象可以使用 SqlSessionFactory 作为构造方法的参数来创建。

```
<
bean
id
=
"sqlSession"
class
=
"org.mybatis.spring.SqlSessionTemplate"
>
<
constructor-arg
index
=
"0"
ref
=
"sqlSessionFactory"
/
>
<
/bean
>
```



