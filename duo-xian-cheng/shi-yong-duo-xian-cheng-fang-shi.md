## 二 使用多线程 {#二-使用多线程}

### 2.1继承Thread类 {#21继承thread类}

MyThread.java

```
public
class
MyThread
extends
Thread
 {
@Override
public
void
run
() {
        
super
.run();
        System.out.println(
"MyThread"
);
    }
}

```

Run.java

```
public
class
Run
 {
public
static
void
main
(String[] args) {
        MyThread mythread = 
new
 MyThread();
        mythread.start();
        System.out.println(
"运行结束"
);
    }

}


```

运行结果：  
![](https://user-gold-cdn.xitu.io/2018/3/20/16243e80f22a2d54?w=161&h=54&f=jpeg&s=7380 "结果")  
从上面的运行结果可以看出：线程是一个子任务，CPU以不确定的方式，或者说是以随机的时间来调用线程中的run方法。

