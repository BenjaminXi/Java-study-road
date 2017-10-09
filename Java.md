# Java基础

### <a id="public和private和protected和默认">public，private，protected和默认有什么区别？</a>
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

### <a id="String&StringBuffer&StringBuilder">String,StringBuffer,StringBuilder有什么区别？</a>
* 可变类方面：String是不可变类，一旦创建，其值将不能被改变；StringBuffer和StringBulider都是可变类；
* 实例化方面：String可以利用构造函数的方式来对其进行初始化，也可以用赋值的方式初始化；StringBuffer只能通过构造函数初始化；
* 线程安全方面：StringBuffer是线程安全的，StringBuilder是线程不安全的；
* 执行效率方面：StringBuilder执行最快，StringBuffer次之，String最低。

### <a id="list&set">list和set有什么区别，各举两种</a>
* list是有序的，可重复的
* set是无序的，不可重复的
list有三种接口：Arraylist，linkedlist，vector；set有两种接口：Hashset和linkedHashset.

### <a id="成员变量&局部变量&实例变量&类变量">什么是类的成员变量，局部变量，实例变量和类变量？</a>
* 类的成员变量即实例变量，定义在类中方法外，存储在堆中，可被对象调用，与对象共存亡，有默认初始值；
* 局部变量定义在方法中，存储在栈中，与方法共存亡，无默认初始值；
* 类变量即静态变量，定义在类中方法外，存储在方法区，可被方法调用，也可被类名调用，与类共存亡，有默认初始值。
[参考1](http://blog.csdn.net/haovip123/article/details/43883109)
[参考2](http://2892931976.blog.51cto.com/5396534/1741592)

### <a id="线程实现">实现线程最常用的两种方式</a>
* 继承Thread类，重写run()方法；
* 实现Runnable接口，并实现run()方法。

### <a id="JSP九大内置对象">jsp九大内置对象</a>
* request,response,pageContext,session,application,out,config,page,exception.

### <a id="Java中&&和&的区别">Java中&&和&的区别</a>
* &&和&都表示与，区别是&&如果不满足第一个表达式，后面就不会再判断；而&需要判断两个条件。


