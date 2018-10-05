#### 什么 是单例模式.

一个类只有一个实例,并提供一个访问他的全局访问点.

#### 为什么要使用单例模式

因为很多对象只需要一个实例，比如线程池、缓存、日志对象等等，所以通过单例模式来构造一个唯一的对象

如何实现

那么，怎么用java实现单例模式呢?

##### 一：类加载的时候实现

`public class Singleton {`

`private static  Singleton  singleton = new Singleton();`

`private Singleton(){`

`}`

`public static Singleton getInstance(){`

`return singleton;`

`}`

`}`

#### 二：类在使用的时候创建

`public class Singleton {`

`private static  Singleton  singleton;`

`private Singleton(){`

`}`

`public static`synchronized `Singleton getInstance(){`

if \(singleton == null\){

`singleton = new Singleton()`  
}

`return singleton;`

`}`

`}`

说明:这个保证了线程安全，但是每次访问都要synchronized来保证线程安全，所以浪费性能.

#### 三: 通过对方法加锁来创建,比上面的性能更加好

`public class Singleton {`

`private  voliate static  Singleton  singleton;`

`private Singleton(){`

`}`

`public static Singleton getInstance(){`

`if (singleton == null){`

`synchronized(Singleton.class){`

`if (singleton == null){`

      `singleton = new Singleton()`

```
}
```

}  
}

`return singleton;`

`}`

`}`

#### 四:通过静态内部类来实现单例

`public class Singleton {`

`private static class SingletonHolder {`

public static final `Singleton singleton = new Singleton();`

}

`private Singleton(){`

`}`

`public static` `Singleton getInstance(){`

`return SingletonHolder.singleton;`

`}`

`}`

五:枚举方式

《Java与模式》中，作者这样写道，使用枚举来实现单实例控制会更加简洁，而且无偿地提供了序列化机制，并由JVM从根本上提供保障，绝对防止多次实例化，是更简洁、高效、安全的实现单例的方式。

六:使用容器 



```
public class SingletonManger{

private static Map<String,Object> objMap = new HashMap<String,Object>();

private SingleManger(){
}

public static getInstatnce(String key){
   return objMap.get(key);
}
}
```



这种事用SingletonManager 将

**多种单例类统一管理**

，在使用时根据key获取对象对应类型的对象。这种方式使得我们可以管理多种类型的单例，并且在使用时可以通过统一的接口进行获取操作，降低了用户的使用成本，也对用户隐藏了具体实现，降低了耦合度。

引用资料:

https://blog.csdn.net/qq\_34337272/article/details/80455972\#24-%E6%87%92%E6%B1%89%E5%BC%8F%E7%99%BB%E8%AE%B0%E5%BC%8F%E9%9D%99%E6%80%81%E5%86%85%E9%83%A8%E7%B1%BB%E6%96%B9%E5%BC%8F





