正如大多数持久层框架一样，MyBatis 同样提供了**一级缓存**和**二级缓存**的支持

1. **一级缓存**: 基于PerpetualCache 的 HashMap本地缓存，其 **存储作用域为 Session**，当**Session flush或close**之后，该**Session中的所有 Cache 就将清空**
2. **二级缓存**与一级缓存其机制相同，默认也是采用 PerpetualCache，HashMap存储，不同在于其**存储作用域为 Mapper\(Namespace\)**，并且**可自定义存储源**，如 Ehcache。

  


