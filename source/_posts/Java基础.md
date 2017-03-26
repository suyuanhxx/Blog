---
title: Java基础
date: 2016-06-21 20:27:53
tags:
---

# Java能力提升计划
主要以J2EE为主线，摆脱迷茫和随波逐流   
这篇文章一定要好好维护，不能copy网上的内容，专表达自己的见解

# TODO List
- Learning English
- 阅读spring源码
- 提高Java知识（基础知识和J2EE相关）
- 读书
- 目前急需提高的技术能力：DI，多线程，ORM映射框架
<!--more-->
## Java语言基础
### 1. java中 `static` , `final`,`transient`,`volatile`关键字的作用
1. `static` 静态修饰关键字，可以修饰变量，程序块，类的方法；当定义一个static的变量的时候jvm会将将其分配在内存堆上，所有程序对它的引用都会指向这一个地址而不会重新分配内存；
2. `final`  只能赋值一次；修饰变量、方法及类。当定义一个final变量时，jvm会将其分配到常量池中，程序不可改变其值；当你定义一个方法时，改方法在子类中将不能被重写；当你修饰一个类时，该类不能被继承。
3. `transient` 一个对象只要实现了Serilizable接口，这个对象就可以被序列化。将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中。
4. `volatile`
### 2. `java.util`相关包  
    集合框架主要包括  
**Collection**   
├List *元素有放入顺序，元素可重复*     
│├LinkedList *双向链表，使用LinkedList可以实现队列`Queue`（包括优先级队列）和栈`Stack`，删除和插入时间复杂度O(1)，查询时间复杂度O(n)*  
│├ArrayList *数组列表，使用频率最高，插入和删除时间复杂度O(n)，查询时间复杂为O(1)*  
│└Vector *线程安全，其他非线程安全*  
│　└Stack  
└Set *元素无放入顺序，元素不可重复，元素去重时可以使用借助set集合操作完成*  
**Map**  * 元素按键值对存储，无放入顺序 *    
├HashMap *最常使用的一种键值对映射数据结构，HashMap内部维护一个线性数组和链表，key为数组，value为链表存储，采用hash算法计算key值，故查询时间复杂度为O(1)，扩容方式要注意*  
hash算法实现无序存放，
├Hashtable *HashMap的线程安全模式，该数据结构已弃用，使用ConcurrentHashMap替代*  
├ConcurrentHashMap *HashMap的线程安全模式，采用分段锁的概念实现Hash线程安全，且在效率上优于‘全局锁’*    
集合框架中非常重要的两个工具类`Collections`和`Arrays`  
`HashMap`线程不安全，主要是多线程`put`，`get`时会出现同步问题  
`HashMap`存储键值对，`HashSet`仅存储对象。`HashSet`内部数据结构使用`HashMap`存储，存储的对象为`key`,`PRESENT`为`value`。`HashSet` `add`代码如下：(`PRESENT`为一个`static final Object`对象)
```
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
```
### 3. Java泛型和反射
### 4. 多线程，高并发。线程池技术`ThreadPool`  
进程和线程之间的区别。

### 5. IO，NIO   
文件读取
step1: `File file = new File("path");`  
step2: `InputStreamReader is = new InputStreamReader(new FileInputStream(file),"UTF-8");`  
step3: `BufferedReader bs = new BufferedReader(is);`  
step4: `String line = bs.readLine();`  
### 6. JVM虚拟机  
### 7. java垃圾回收机制   
[垃圾回收面试技巧](https://www.zhihu.com/question/35164211) 
内存溢出（不能被GC）：检查List、MAP等集合对象是否有使用完后，未清除的问题。List、MAP等集合对象会始终存有对对象的引用，使得这些对象不能被GC回收。  
为什么要垃圾回收  
回收对象：不使用的对象；超出作用域的对象/引用计数为空的对象；从gc root开始搜索，搜索不到的对象；从root搜索不到，而且经过第一次标记、清理后，仍然没有复活的对象。  
垃圾回收时间：系统空闲的时候，系统自身决定，不可预测的时间/调用System.gc()的时候，  
垃圾回收方式：引用计数；根搜索算法（GC Root Tracing）  
垃圾回收算法  

---
## J2EE
- Servlet和Servlet容器
- EJB
- Tomcat JBoss Jetty热部署
- Spring依赖注入DI Lookup
---
## 数据结构&&数据库
- 常用数据结构，列表，链表，队列，堆，二叉树
- mysql数据引擎，mysql锁机制
- 数据库表设计范式
---
## 软件架构
- 设计模式
- Spring框架，SpringAOP Spring DI
- SpringMVC
- ORM映射框架，mybatis
- Redis缓存
- 远程调用框架Hessian
- 分布式Dubbo和zookeeper
---
## 操作系统&&网络编程
- TCP/IP
- Socket编程
