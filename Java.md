#Java笔试面试精选

##数据结构
####数组和链表什么区别
* 存储方式不同：数组是将元素在内存中连续存放，由于每个元素占用内存相同，可以通过下标迅速访问数组中任何元素；链表恰好相反，链表中的元素在内存中不是顺序存储的，而是通过存在元素中的指针联系到一起。比如：上一个元素有个指针指到下一个元素，以此类推，直到最后一个元素。如果要访问链表中一个元素，需要从第一个元素开始，一直找到需要的元素位置。
* 增加删除方式不同：数组中增加一个元素，需要移动大量元素，在内存中空出一个元素的空间，然后将要增加的元素放在其中。同样的道理，如果想删除一个元素，同样需要移动大量元素去填掉被移动的元素。如果应用需要快速访问数据，很少或不插入和删除元素，就应该用数组。链表中增加和删除一个元素非常简单，只要修改元素中的指针就可以了。如果应用需要经常插入和删除元素你就需要用链表数据结构了。

####堆和栈有什么区别和联系
* 分配释放方式不同：堆是由编译器自动分配释放，栈由程序员分配释放；
* 存放不同：堆用于存放对象，栈用于执行程序；
* 线程共享不同：堆可以被多个线程共享，栈不可以被多个线程共享；
* 存储空间不同：堆空间不连续，栈空间连续；
* 读取速度不同：堆速度慢，栈速度快。
* 生存期不同：栈的生存期是确定的，因此缺乏一定的灵活性；堆在运行时动态分配内存，生存期不用提前告诉编译器，导致读取速度慢。

####根据前序遍历和后序遍历求中序遍历
无法确定唯一的二叉树

####如何用34,76,45,18,26,54,92,65构建二叉搜索树，并求树的深度

####时间复杂度最好的为O(n)的是,时间复杂度最坏的为O(n\*n) 的是,稳定的排序有,
A快速排序 B基数排序 C堆排序 D归并排序 E冒泡排序

####用递归实现深度优先算法

####实现进程的方法

####进程与线程的联系与区别

####sleep和wait的区别

####cookie与session的区别
* cookie机制采用的是在客户端保持状态的方案，其作用是是为了解决HTTP无状态的缺陷所做的努力，即数据保存在客户端；而session采用的是保存在服务器端保持状态的方案，数据放在服务器上；
* cookie安全性不够，cookie放在客户端，其他人可以进行cooke欺骗；而session放在服务器端，因此比较安全；
* cookie性能更高一些；而session放在服务器上，当访问量增加时，会降低服务器性能；
* cookie保存的数据不超过4K，最多20个cookie；而session不存在这个问题。

####散列表

####链表反转

##Java基础

####public，private，protected和默认有什么区别？
* private：除了包含该成员的类外，其他类无法访问这个成员；
* 默认访问权限为包访问权限，意味着当前包中的所有其他类对该成员都有访问权限，但对于其他包这个成员是private；
* protected为继承访问权限，也提供包访问权限；
* public为接口访问权限，表明该数据成员、成员函数是对所有用户开放的，所有用户都可以直接进行调用；

 修饰符  |  类内部 |  同个包（package） |  子类 |  其他范围 
------------- | ------------- | -------------| -------------| -------------
public | Y |  Y |  Y |  Y
protected  |  Y |  Y |  Y |  N
无修饰符  |  Y |  Y |  N or Y(见说明） |  N
private  |  Y |  N |  N |  N

####String,StringBuffer,StringBuilder有什么区别？
* 可变类方面：String是不可变类，一旦创建，其值将不能被改变；StringBuffer和StringBulider都是可变类；
* 实例化方面：String可以利用构造函数的方式来对其进行初始化，也可以用赋值的方式初始化；StringBuffer只能通过构造函数初始化；
* 线程安全方面：StringBuffer是线程安全的，StringBuilder是线程不安全的；
* 执行效率方面：StringBuilder执行最快，StringBuffer次之，String最低。

####list和set有什么区别，各举两种
* list是有序的，可重复的
* set是无序的，不可重复的
list有三种接口：Arraylist，linkedlist，vector；set有两种接口：Hashset和linkedHashset.

####什么是类的成员变量，局部变量，实例变量和类变量？
* 类的成员变量即实例变量，定义在类中方法外，存储在堆中，可被对象调用，与对象共存亡，有默认初始值；
* 局部变量定义在方法中，存储在栈中，与方法共存亡，无默认初始值；
* 类变量即静态变量，定义在类中方法外，存储在方法区，可被方法调用，也可被类名调用，与类共存亡，有默认初始值。
[参考1](http://blog.csdn.net/haovip123/article/details/43883109)
[参考2](http://2892931976.blog.51cto.com/5396534/1741592)

####实现线程最常用的两种方式
* 继承Thread类，重写run()方法；
* 实现Runnable接口，并实现run()方法。

####jsp九大内置对象
* request,response,pageContext,session,application,out,config,page,exception.

##数据库
####什么是事务
* 事务是数据库中一个单独的执行单元，当在数据库中更改数据成功时，在事务中的数据便会提交，不再改变。否则，事务取消或者回滚，更改无效。
* 事务必须满足4个特性：原子性，一致性，隔离型，持久型。

####数据库的原子性
* 事务是一个不可分割的整体，事务具有原子性，即当数据修改时，要么全执行，要么全不执行，即不允许事务部分完成，事务必须完整地执行。

####如何实现数据库的分页查询
* limit语句

####各种范式有什么区别？
* 常见的范式有1NF,2NF,3NF,BCNF,4NF;
* 1NF第一范式，指数据库的每一列都是不可分割的基本数据项，同一列中不能有多个值，如果出现多个属性，就可能需要重新定义一个新的实体。简而言之，第一范式是无重复的列;
* 2NF第二范式，是在第一范式的基础上建立起来的，要求每行或实例必须可以被唯一地区分;
* 3NF第三范式，

###编程题
####一串字母数字符号混合的字符串，输出小写字母
####输入逗号分割的数字，输出被除数。如输入2,4,6,8,10,3,9;输出4,6,8,10,9.
####输入“I am a student.” 实现输出"student. a am I".
####对称的字符串的最大长度
####rand5可以随机产生1到5的一个整数，如何用rand5构建rand7，使其能随机产生1到7的一个整数。

##设计模式
####什么是工厂模式

####单例模式
我们在应用程序中保持一个唯一的实例，如：IO处理，数据库操作等，由于这些对象都要占用重要的系统资源，所以我们必须限制这些实例的创建或始终使用一个公用的实例，这就是单例模式，一个类只有一个实例。</br>
单例模式有许多不同的实现，但这些实现有以下共同点：
* 构造参数为私有，这样可以防止其他类实例化
* 单例类被定义为sealed，这样就不会被继承
* 一个静态的变量用来保存单实例的引用
* 一个公有的静态方法用来获取单实例的引用，如果实例为null即创建一个

#####单线程环境
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
#####多线程环境
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
#####多线程改进
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
#####静态构造函数
```
public sealed class Singleton{
 private Singleton(){}
 private static Singleton instance = new Singleton();
 public static Singleton Instance{
  get{
   return instance;
  }
 }
}
```
这个不太理解，待更新。

##linux
####重定向至文件时，>与>>有什么区别

##软件工程
####需求分析
####UML
