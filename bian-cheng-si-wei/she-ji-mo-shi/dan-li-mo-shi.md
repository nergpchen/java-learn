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

三:

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

