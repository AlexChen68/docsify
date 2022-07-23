## 概述

`LinkedList` 同时实现了 `List` 接口和 `Deque` 接口，它既可以当成顺序容器，又可以作为双端队列使用，同时还可以看作一个栈（Stack）。栈和队列还有一个更好的选择是 `ArrayDeque`，它有比 `LinkedList` 更好的性能。

## 类图

![LinkedList类图](../../../images/java/collection/linkedlist-class.png)

`LinkedList` 实现了四个接口：

* `java.util.List` List 接口
* `java.io.Serializable` 序列化接口
* `java.lang.Cloneable` 可克隆接口
* `java.util.Deque` 双端队列接口

另外，`LinkedList` 继承了 `java.util.AbstractSequentialList` 抽象类，它是 `AbstracList` 的子类，实现了只能**连续**访问“数据存储” 等随机操作的方法

## 属性



## 构造方法



## 方法