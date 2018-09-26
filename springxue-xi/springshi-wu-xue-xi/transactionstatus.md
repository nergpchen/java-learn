TransactionStatus:

TransactionStatus接口用来记录事务的状态 该接口定义了一组方法,用来获取或判断事务的相应状态信息.



public

interface

TransactionStatus

{ 

boolean

isNewTransaction

\(\)

; 

// 是否是新的事物

boolean

hasSavepoint

\(\)

; 

// 是否有恢复点

void

setRollbackOnly

\(\)

; 

// 设置为只回滚

boolean

isRollbackOnly

\(\)

; 

// 是否为只回滚

boolean

 isCompleted; 

// 是否已完成

 }



