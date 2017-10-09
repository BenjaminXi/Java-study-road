# 操作系统
### 实现进程的方法
### <a id="进程与线程">进程与线程的联系与区别</a>
* 进程的概念：是具有一定独立功能的程序在某个数据集合上的一次运行活动，是系统进行资源分配和调度的一个独立单位；
* 线程的概念：是进程的一个实体，是CPU调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。线程自己基本上不拥有系统资源，只拥有一点在运行中必不可少的资源（如程序计数器，寄存器和栈），与同属一个进程的其他线程共享进程的全部资源。
* 一个程序至少有一个进程，一个进程至少有一个线程；
* 执行过程不同：进程在执行过程中有独立的内存单元，而多个线程是共享内存，从而有较高的运行效率；线程在执行过程中与进程是有区别的，每个线程都有一个程序运行的入口，执行序列和出口，但是线程不能够独立运行，必须依存在应用程序中，由应用程序提供多个线程执行控制。
* 最主要的区别是资源管理方式不同：进程有独立的地址空间，一个进程崩溃后，在保护模式下不会对其它进程产生影响，而线程只是一个进程中的不同执行路径。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。

### <a id="进程间的通信方式程">进程间的通信方式</a>
* 管道（pipe）：管道是一种半双工的通信方式，数据只能单向流动，而且只能在具有亲缘关系的进程间使用。进程的亲缘关系通常是指父子进程关系；
* 有名通道：也是半双工的通信方式，但是它允许无亲缘关系进程间的通信。
* 信号量：是一个计数器，可以用来控制多个进程对共享资源的访问，主要作为进程间以及同一进程内不同线程之间的同步手段。
* 消息队列：是由消息的链表，存放在内核中并由消息队列标识符标识。
* 信号：用于通知接收进程某个事件已经发生。
* 共享内存：是最快的进程间通信方式，往往与信号量配合使用，来实现进程间的同步和通信。
* 套接字：可用于不同机器间的进程通信。

### sleep和wait的区别

### <a id="单线程环境">单线程环境</a>
```
public sealed class Singleton{
 private Singleton(){} //私有构造函数
 private static Singleton instance = null; //一个静态的变量用来保存单实例的引用
 public static Singleton Instance{
  get{
   if(instance == null)
    instance = new Singleton();
    return instance;
  }
 }
}
```
缺点：如果有两个线程判断instance为null,那么都会创建一个实例，就不满足单例模式了。为此需要添加一个同步锁，在if语句之前添加锁，这样一个时刻只能有一个线程得到同步锁。
### <a id="多线程环境">多线程环境</a>
```
public sealed class Singleton{
 private Singleton(){} //私有构造函数
 private static Singleton instance = null; //一个静态的变量用来保存单实例的引用
 private static readonly object syncObj = new object(); //定义一个同步锁
 public static Singleton Instance{
  get{
   lock(syncObj){
    if(instance == null)
     instance = new Singleton();
     return instance;
     }
  }
 }
}
```
缺点：但是加锁是一个非常耗时的操作，加锁的目的是为了创建实例，如果实例存在，就不要饭后；如果实例不存在，再加锁。
### <a id="多线程改进">多线程改进</a>
```
public sealed class Singleton{
 private Singleton(){} //私有构造函数
 private static Singleton instance = null; //一个静态的变量用来保存单实例的引用
 private static readonly object syncObj = new object(); //定义一个同步锁
 public static Singleton Instance{
  get{
   if(instance==null){
    lock(syncObj){
     if(instance == null)
      instance = new Singleton();
      }
     }
     return instance;
  }
 }
}
```
