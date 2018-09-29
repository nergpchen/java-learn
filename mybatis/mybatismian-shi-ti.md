1、\#{}和${}的区别是什么？

```
#{}是预编译处理，${}是字符串替换。
Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；
Mybatis在处理${}时，就是把${}替换成变量的值。
使用#{}可以有效的防止SQL注入，提高系统安全性。
```

当实体类中的属性名和表中的字段名不一样 ，怎么办 ？

```
第1种： 通过在查询的sql语句中定义字段名的别名，让字段名的别名和实体类的属性名一致
```

```
<
select
 id=”selectorder” parametertype=”int” resultetype=”
me
.gacl.domain.
order
”
>
select
 order_id id, order_no orderno ,order_price price form orders 
where
 order_id=
#{id}; 
<
/
select
>
```

```
第2种： 通过< resultMap >来映射字段名和实体类属性名的一一对应的关系
```

3、 模糊查询like语句该怎么写?

第1种：在Java代码中添加sql通配符。

```
第2种：在sql语句中拼接通配符，会引起sql注入
```

4.通常一个Xml映射文件，都会写一个Dao接口与之对应，请问，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗？

Dao接口，就是人们常说的Mapper接口，接口的全限名，就是映射文件中的namespace的值，接口的方法名，就是映射文件中MappedStatement的id值，接口方法内的参数，就是传递给sql的参数。  
   Mapper接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为key值，可唯一定位一个MappedStatement，在Mybatis中，每一个标签，都会被解析为一个MappedStatement对象。  
   Dao接口里的方法，是不能重载的，因为是全限名+方法名的保存和寻找策略。  
    Dao接口的工作原理是JDK动态代理，Mybatis运行时会使用JDK动态代理为Dao接口生成代理proxy对象，代理对象proxy会拦截接口方法，转而执行MappedStatement所代表的sql，然后将sql执行结果返回。

5、Mybatis是如何进行分页的？分页插件的原理是什么？

```
Mybatis使用RowBounds对象进行分页，它是针对ResultSet结果集执行的内存分页，而非物理分页，可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。

分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，
根据dialect方言，添加对应的物理分页语句和物理分页参数。
```

6、Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？

```
答：
第一种是使用<resultMap>标签，逐一定义列名和对象属性名之间的映射关系。

第二种是使用sql列的别名功能，将列别名书写为对象属性名，比如T_NAME AS NAME，对象属性名一般是name，小写，
但是列名不区分大小写，Mybatis会忽略列名大小写，智能找到与之对应对象属性名，你甚至可以写成T_NAME AS NaMe，
Mybatis一样可以正常工作。
有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。
```

7.如何执行批量插入?

&lt;insert id="insertList" parameterType="list" &gt;

replace into xx \(id, c1,c2\) values

&lt;foreach collection="list" item="it" separator=","&gt;  
&lt;/foreach&gt;

这篇文章有详细的介绍:[https://blog.csdn.net/luo4105/article/details/77892889](https://blog.csdn.net/luo4105/article/details/77892889)

10、Mybatis动态sql是做什么的？都有哪些动态sql？能简述一下动态sql的执行原理不？  
`Mybatis动态sql可以让我们在Xml映射文件内，以标签的形式编写动态sql，完成逻辑判断和动态拼接sql的功能。 Mybatis提供了9种动态sql标签：trim|where|set|foreach|if|choose|when|otherwise|bind。 其执行原理为，使用OGNL从sql参数对象中计算表达式的值，根据表达式的值动态拼接sql，以此来完成动态sql的功能。`

* 11、Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？

```
不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置namespace，那么id不能重复；毕竟namespace不是必须的，只是最佳实践而已。

原因就是namespace+id是作为Map<String, MappedStatement>的key使用的，如果没有namespace，就剩下id，那么，id重复会导致数据互相覆盖。有了namespace，自然id就可以重复，namespace不同，namespace+id自然也就不同。
```

12.讲下MyBatis的缓存

MyBatis的缓存分为一级缓存和二级缓存,一级缓存放在session里面,默认就有,二级缓存放在它的命名空间里,默认是不打开的,使用二级缓存属性类需要实现Serializable序列化接口\(可用来保存对象的状态\),可在它的映射文件中配置

13.主键生存策略  
 ** 1**、数据库支持自动生成主键

　　若数据库支持自动生成主键的字段（比如 MySQL和 SQL Server），则可以设置useGeneratedKeys=”true”，然后再把keyProperty 设置到目标属性上。

* mysql 支持自增主键，自增主键值的获取，
  mybatis 也是利用statement.getGenreatadKeys\(\);
* useGeneratedKeys="true” 使用自增主键获取主键值策略。
* keyProperty: 将获取到的自增主键值放到 Javabean 哪一个属性值中。

&lt;insert id="addEmployee" useGeneratedKeys="true" keyProperty="id" databaseId="mysql"&gt;

 insert into employee\(last\_name,age,email\)

 values\(\#{lastName},\#{age},\#{email}\)

&lt;/insert&gt;

  


**2**、数据库不支持自动生成主键

　　而对于不支持自增型主键的数据库（例如Oracle），则可以使用 selectKey 子元素：selectKey 元素将会首先运行，id 会被设置，然后插入语句会被调用。

&lt;insert id="addEmployee" databaseId="oracle"&gt;&lt;selectKey keyProperty="id" order="BEFORE" resultType="Integer"&gt; select EMPLOYEE\_SEQ.nextval from dual &lt;/selectKey&gt;&lt;!-- 插入的主键是从序列中获取的 --&gt; insert into employee\(id,last\_name,age,email\) values\(\#{id},\#{lastName},\#{age},\#{email}\)&lt;/insert&gt;



###### 25、Mybatis中如何执行批处理？

答：使用BatchExecutor完成批处理。

###### 26、Mybatis都有哪些Executor执行器？它们之间的区别是什么？

答：Mybatis有三种基本的Executor执行器，SimpleExecutor、ReuseExecutor、BatchExecutor。1）SimpleExecutor：每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。2）ReuseExecutor：执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map3）BatchExecutor：完成批处理。

###### 27、Mybatis中如何指定使用哪一种Executor执行器？

答：在Mybatis配置文件中，可以指定默认的ExecutorType执行器类型，也可以手动给DefaultSqlSessionFactory的创建SqlSession的方法传递ExecutorType类型参数。

###### 28、Mybatis执行批量插入，能返回数据库主键列表吗？



