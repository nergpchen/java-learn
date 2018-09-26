Spring事务接口:

* **PlatformTransactionManager:**（平台）事务管理器
* **TransactionDefinition： **事务定义信息\(事务隔离级别、传播行为、超时、只读、回滚规则\)
* **TransactionStatus： **事务运行状态

1.**PlatformTransactionManager：**

PlatformTransactionManager接口中定义了三个方法：

```
Public interface 
PlatformTransactionManager
()
...
{  
    
// Return a currently active transaction or create a new one, according to the specified propagation behavior（根据指定的传播行为，返回当前活动的事务或创建一个新事务。）
TransactionStatus getTransaction (TransactionDefinition definition)
throws TransactionException
; 
    
// Commit the given transaction, with regard to its status（使用事务目前的状态提交事务）
Void commit (TransactionStatus status)
throws
 TransactionException
;  
    
// Perform a rollback of the given transaction（对执行的事务进行回滚）
Void  rollback
(TransactionStatus status)
throws
 TransactionException
;    } 

```

  




