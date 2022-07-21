##  概述

ArrayList ，基于 `[]` 数组实现的，支持**自动扩容**的动态数组。

## 类图

![ArrayList类图](../../../images/java/collection/arraylist-class.png ':size=60%')

`ArrayList` **实现**了 4 个接口，分别是：

* `java.lang.Cloneable` 接口，表示 ArrayList 支持克隆。
* `java.util.RandomAccess` 接口，表示 ArrayList 支持**快速**的随机访问。
* `java.io.Serializable` 接口，表示 ArrayList 支持序列化的功能。
* `java.util.List` 接口，提供数组的添加、删除、修改、迭代遍历等操作。

同时还**继承**了 `java.util.AbstractList` 抽象类，`AbstractList` 类提供了一些集合的默认实现。

## 属性

类属性

```java
// 默认初始容量
private static final int DEFAULT_CAPACITY = 10;

// 用于空实例的共享空数组实例（数组不指定容量时使用）
private static final Object[] EMPTY_ELEMENTDATA = {};

// 用于默认大小的空实例的共享空数组实例。我们将其与 EMPTY_ELEMENTDATA 区分开来，以了解添加第一个元素时要膨胀多少
private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

// 要分配的数组的最大大小。一些 VM 在数组中保留一些标题字。尝试分配更大的数组可能会导致 OutOfMemoryError：请求的数组大小超过 VM 限制
private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
```

实例属性

```java
// 存储 ArrayList 元素的数组缓冲区。 ArrayList 的容量就是这个数组缓冲区的长度。当添加第一个元素时，任何具有 elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA 的空 ArrayList 都将扩展为 DEFAULT_CAPACITY。
transient Object[] elementData;

// ArrayList 的大小（它包含的元素数量）
private int size;
```

## 构造方法

1. 无参构造时：使用默认空数组属性 `DEFAULTCAPACITY_EMPTY_ELEMENTDATA`

```java
public ArrayList() {
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}
```

2. 指定容量构造：如果容量大于 0，直接创建指定容量的对象数组；如果初始化容量为 0 时，使用 `EMPTY_ELEMENTDATA` 空数组，在向集合添加元素时，再进行扩容。

```java
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        // 初始化容量大于 0 时，创建 Object 数组
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        // 初始化容量等于 0 时，使用 EMPTY_ELEMENTDATA 对象
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        throw new IllegalArgumentException("Illegal Capacity: " + initialCapacity);
    }
}
```

3. 按照集合的迭代器返回的顺序构造一个包含指定集合元素的列表：

```java
public ArrayList(Collection<? extends E> c) {
    // 先将指定集合转换为 Object 数组（实际上在 JDK9之前，数组 a 的实际类型为原集合的类型）
    Object[] a = c.toArray();
    if ((size = a.length) != 0) {
        // 由于 a 的类型不一致，需要先判断；不一致时需要先转为 Object 数组再赋值
        if (c.getClass() == ArrayList.class) {
            elementData = a;
        } else {
            elementData = Arrays.copyOf(a, size, Object[].class);
        }
    } else {
        // 指定集合为空，使用空数组
        elementData = EMPTY_ELEMENTDATA;
    }
}
```

在 `ArrayList` 未指定容量或集合时，其初始化完成后，内部数组为 `DEFAULTCAPACITY_EMPTY_ELEMENTDATA`空数组，这样是为了节省内存；之所以使用 `DEFAULTCAPACITY_EMPTY_ELEMENTDATA` 和 `EMPTY_ELEMENTDATA` 两个空数组，是为了区别扩容，前者用于未指定容量时使用，首次扩容时会扩容至 10，而后者用于指定容量为 0 时使用，首次扩容时会按照 **1.5 倍**扩容从 0 开始而不是 10。

## 方法

### 添加单个元素

添加到数组末尾 `add(E e)`

```java
public boolean add(E e) {
    // 
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}
```

添加到指定顺序 `add(int index, E element)`

```java
public void add(int index, E element) {
    rangeCheckForAdd(index);
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    System.arraycopy(elementData, index, elementData, index + 1, size - index);
    elementData[index] = element;
    size++;
}
```

当向数组添加元素前，都执行了 `ensureCapacityInternal(int minCapacity)` 方法，来确保数组有足够的容量容纳新添加的元素，具体代码如下：

```java
// 计算需要扩容的容量
private static int calculateCapacity(Object[] elementData, int minCapacity) {
    // 当数组为默认空数组，即初始化时未指定容量时
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        // 待扩容的最小数组容量 和 默认容量 10 两者取大者
        return Math.max(DEFAULT_CAPACITY, minCapacity);
    }
    // 否则扩容至指定容量
    return minCapacity;
}

// 计算需要扩容的容量并扩容
private void ensureCapacityInternal(int minCapacity) {
    ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}

// 执行数组扩容
private void ensureExplicitCapacity(int minCapacity) {
    modCount++;
    // overflow-conscious code
    if (minCapacity - elementData.length > 0)
        // 数组扩容
        grow(minCapacity);
}
```

### 数组扩容

```java
// 增加容量以确保它至少可以容纳最小容量参数指定的元素数量
private void grow(int minCapacity) {
    // 保存旧容量
    int oldCapacity = elementData.length;
    // 新容量 = 1.5 倍旧容量
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    // 指定容量大于 1.5 倍旧容量，则扩容至指定容量
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    // 判断是否超出最大可扩容容量
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        // 扩容至整型最大值 或 最大可扩容量 MAX_ARRAY_SIZE
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    // 扩容
    elementData = Arrays.copyOf(elementData, newCapacity);
}

// 计算超大扩容容量：最小容量超过最大可扩容量，扩容至整型最大值，否则扩容至最大可扩容量
private static int hugeCapacity(int minCapacity) {
    if (minCapacity < 0) // overflow
        throw new OutOfMemoryError();
    // MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8
    return (minCapacity > MAX_ARRAY_SIZE) ? Integer.MAX_VALUE : MAX_ARRAY_SIZE;
}
```

###  添加多个元素

批量添加多个元素 `addAll(Collection<? extends E> c)`，在明确知道需要添加多少元素的前提下，使用本方法可减少扩容次数。

```java
public boolean addAll(Collection<? extends E> c) {
    Object[] a = c.toArray();
    int numNew = a.length;
    ensureCapacityInternal(size + numNew);  // Increments modCount
    System.arraycopy(a, 0, elementData, size, numNew);
    size += numNew;
    return numNew != 0;
}
```