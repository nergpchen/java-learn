### 一Mybatis是什么？

 Mybatis是持久层框架，支持定制sql、存储过程、以及高级映射.  
MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs\(Plain Old Java Objects,普通的 Java对象\)映射成数据库中的记录。

### Mybatis怎么用?

每个基于 MyBatis 的应用都是以一个 SqlSessionFactory 的实例为中心的。SqlSessionFactory 的实例可以通过 SqlSessionFactoryBuilder 获得。而 SqlSessionFactoryBuilder 则可以从 XML 配置文件或一个预先定制的 Configuration 的实例构建出 SqlSessionFactory 的实例。

String

```
 String resource =
"org/mybatis/example/mybatis-config.xml"
;
InputStream inputStream =Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

```

Mybatis

