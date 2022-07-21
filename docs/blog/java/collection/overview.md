# Java集合框架概览

容器，就是可以容纳其他Java对象的对象。*Java Collections Framework(JCF)* 为Java开发者提供了通用的容器，其始于JDK 1.2，优点是:

- 降低编程难度

- 提高程序性能

- 提高API间的互操作性

- 降低学习难度

- 降低设计和实现相关API的难度

- 增加程序的重用性


Java容器里只能放对象，对于基本类型(int, long, float, double等)，需要将其包装成对象类型后(Integer, Long, Float, Double 等)才能放到容器里。很多时候拆包装和解包装能够自动完成。这虽然会导致额外的性能和空间开销，但简化了设计和编程。

Java容器主要包括 Collection 和 Map 两种，Collection 存储着对象的集合，而 Map 存储着键值对(两个对象)的映射表：

1. Collection：主要由 List、Set、Queue 组成。
    - List 代表有序、可重复的集合，典型代表就是封装了动态数组的 ArrayList 和封装了链表的 LinkedList；
    - Set 代表无序、不可重复的集合，典型代表就是 HashSet 和 TreeSet；
    - Queue 代表队列，典型代表就是双端队列 ArrayDeque，以及优先级队列 PriorityQue。
2. Map：代表键值对的集合，典型代表就是 HashMap。

![Java集合框架](../../../images/java/collection/overview-framework.png ':size=60%')

## Collection接口

`Collection` 是所有序列集合共有的根接口。集合表示一组对象，称为其元素。一些集合允许重复元素，而另一些则不允许。有些是有序的，有些是无序的。 JDK 不提供此接口的任何直接实现：它提供更具体的子接口（如 Set 和 List）的实现。此接口通常用于传递集合并在需要最大通用性的地方操作它们。

`Collection`接口继承了 `Iterable`接口，实现 `Collection` 就意味着需要提供 `iterator()` 方法

`java.util.AbstractCollection` 类提供了 `Collection` 类的默认实现，使得你可以创建 `AbstractCollection` 的子类型，而其中没有不必要的代码重复

### List接口

#### ArrayList

ArrayList 底层是由数组实现的，支持随机存取，也就是可以通过下标直接存取元素；

如果内部数组的容量不足时会自动扩容，因此当元素非常庞大的时候，效率会比较低。

#### Vector

和 ArrayList 类似，但它是线程安全的。

#### LinkedList



### Queue



### Set



## Map接口


## 参考资料

[Java 程序员进阶之路](https://tobebetterjavaer.com/collection/gailan.html)
[Java全栈知识体系](https://pdai.tech/md/java/collection/java-collection-all.html)