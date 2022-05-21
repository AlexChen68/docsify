## 设计原则

### 单一职责原则SRP

> Single-Responsibility Principle，就一个类而言，应该仅有一个引起它变化的原因，通俗的说，就是一个类只负责一项职责。此原则的核心就是**解耦**和**增强内聚性**。
>
> 类的职责主要包括两个方面: 数据职责和行为职责，数据职责通过其属性来体现，而行为职责通过其方法来体现。
>
> 如果一个类承担的职责过多，就等于把这些职责耦合在一起，一个职责的变化可能会削弱或者抑制这个类完成其他职责的能力。这种耦合会导致脆弱的设计，可复用的可能性就越小。
>
> 一个类只有一个引起它变化的原因，否则就应当考虑重构，是否重构由引起变化的原因决定，而不由功能决定。虽然职责常常引起变化的轴线，但有时就未必，应该适当考虑；可以通过Facade模式或Proxy模式进行职责分离。

优点：

1. 降低类的复杂度；

2. 提高类的可读性，提高系统的可维护性；

3. 降低变更引起的风险（降低对其他功能的影响）。

例子：

SpringMVC 中Entity,DAO,Service,Controller, Util等的分离。

### 开闭原则OCP

> Open Close Principle，开闭原则就是说**对扩展开放，对修改关闭**。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。所以一句话概括就是：为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用**接口**和**抽象类**。

例子：

设计模式中模板方法模式和观察者模式。

### 里氏代换原则LSP

> Liskov Substitution Principle，所有引用基类(父类)的地方必须能透明地使用其子类的对象，即子类能够必须能够替换基类能够从出现的地方，子类也能在基类的基础上新增行为。
>
>  LSP是继承复用的基石，是对“开-闭”原则的补充。实现“开-闭”原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。
>
> 里氏代换原则是实现开闭原则的重要方式之一，由于使用基类对象的地方都可以使用子类对象，**因此在程序中尽量使用基类类型来对对象进行定义，而在运行时再确定其子类类型，用子类对象来替换父类对象**。

例子：

正方形是长方形。

### 接口隔离原则ISL

> (Interface Segregation Principle，ISL): 客户端不应该依赖那些它不需要的接口。(这个法则与迪米特法则是相通的)。
>
> 一旦一个接口太大，则需要将它分割成一些更细小的接口，使用该接口的客户端仅需知道与之相关的方法即可。 注意，在该定义中的接口指的是所定义的方法。例如外面调用某个类的public方法。这个方法对外就是接口。
>

### 依赖倒转原则DIP

> Dependency-Inversion Principle 要依赖抽象，而不要依赖具体的实现，具体而言就是高层模块不依赖于底层模块，二者共同依赖于抽象。抽象不依赖于具体，具体依赖于抽象。
>
> 实现开闭原则的关键是抽象化，并且从抽象化导出具体化实现，如果说开闭原则是面向对象设计的目标的话，那么依赖倒转原则就是面向对象设计的主要手段。

### 其他原则-合成复用原则

> Composite Reuse Principle，合成复用原则就是指在一个新的对象里通过关联关系（包括组合关系和聚合关系）来使用一些已有的对象，使之成为新对象的一部分；新对象通过委派调用已有对象的方法达到复用其已有功能的目的。简言之：**要尽量使用组合/聚合关系，少用继承**。

### 其他原则-迪米特法则（最少知道原则）

> Demeter Principle，为什么叫最少知道原则，就是说：一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立，这样，当一个模块修改时，就会尽量少的影响其他的模块，扩展会相对容易，这是对软件实体之间通信的限制，它要求限制软件实体之间通信的宽度和深度。
>
> 在迪米特法则中，对于一个对象，其关联的实体包括以下几类:
>
> 1. 当前对象本身(this)；
> 2. 以参数形式传入到当前对象方法中的对象；
> 3. 当前对象的成员对象（包括集合中的元素）；
> 4. 当前对象所创建的对象。

例子：

外观模式Facade(结构型)

## 创建型模式

### 简单工厂(Simple Factory)

**定义**

> 定义一个工厂类，可以根据传入的参数不同创建不同类实例，被创建的实例通常都有相同的父类。 简单工厂模式在java中得到了大量的使用，它属于创建型的设计模式，但是它不属于GOF23设计模式中的一种。
>
> 工厂模式提供公共的接口，客户端直接使用公共接口来创建对象，客户端这边不关心对象是怎么创建的，其中包含3个角色：工厂角色，抽象产品角色，具体产品角色。
> 工厂角色是简单工厂模式的核心，负责产品实例的内部逻辑；
> 抽象产品角色是所有具体产品角色的父类，封装了公共的方法；
> 具体产品角色是工厂角色创建的目标对象。
>
> 因为简单工厂模式将对象的创建和使用分离，使得系统更加符合单一职责原则。

**适用场景**

1. 工厂类创建的对象比较少；
2. 客户端只需要传入某个参数，对如何创建对象不关心。

**优点**

1. 只需要传入参数就可以获取到需要的对象，客户端使用简单；
2. 通过反射或者配置文件，可以在不修改任何代码的情况下更换或者新增产品类，提供系统的灵活性；
3. 让创建和使用进行分离。

**缺点**

1. 工厂类的职责比较重，如果新增一些类，需要修改工厂类判断逻辑，违背了开闭原则；
2. 增加类的个数，增加系统的复杂性和理解难度。

**代码示例**

```java
public interface Mobile {
    void produce();
}
public class IphoneMobile implements Mobile{
    public void produce() {
        System.out.println("生产苹果手机");
    }
}
public class HuaweiMobile implements Mobile{
    public void produce() {
        System.out.println("生产华为手机");
    }
}
public class FoxconnFactory {
    public Mobile getMobile(String mobileType){
        if("iphone".equals(mobileType)){
            return new IphoneMobile();
        }else if("huawei".equals(mobileType)){
            return new HuaweiMobile();
        }
        return null;
    }
}
public class SimpleFactoryTest {
    public static void main(String[] args) {
        FoxconnFactory foxconnFactory = new FoxconnFactory();
        Mobile mobile = foxconnFactory.getMobile("iphone");
        mobile.produce();
        Mobile huawei = foxconnFactory.getMobile("huawei");
        huawei.produce();
    }
}
```



### 工厂方法(Factory Method)

**定义**

> 定义了一个创建对象的接口，但由工厂子类决定要实例化哪个类。工厂方法把实例化操作推迟到工厂的子类。

**适用场景**

1. 在任何需要生成**复杂对象**的地方，都可以使用工厂方法模式。直接用**new**可以完成的**不需要用工厂模式**个人理解，重点就是这个复杂 （构造函数有很多参数）和 是否可以 直接用new。
2. 客户端只知道传入工厂类的参数，对于如何创建对象并不关心。
3. 工厂类负责创建的对象比较少，由于创建的对象较少，不会造成工厂方法中的业务逻辑太过复杂。

**优点**

1. 用户只需要关心所需产品的对应工厂，无需关心细节；
1. 完全支持开闭原则，提高可扩展性。所谓的开闭原则就是对扩展开放，对修改关闭，再说白点就是实现工厂方法以后要进行扩展时不需要修改原有代码，只需要增加一个工厂实现类和产品实现类就可以。这样的好处可以降低因为修改代码引进错误的风险。

**缺点**

1. 加入一种产品，会创建一个具体工厂类和具体产品类，因此，类的个数容易过多，增加复杂度；
1. 抽象工厂和抽象产品增加了系统的抽象性和理解难度。

**代码示例**

```java
public interface FoodFactory {
    Food makeFood(String name);
}
public class ChineseFoodFactory implements FoodFactory {

    @Override
    public Food makeFood(String name) {
        if (name.equals("A")) {
            return new ChineseFoodA();
        } else if (name.equals("B")) {
            return new ChineseFoodB();
        } else {
            return null;
        }
    }
}
public class AmericanFoodFactory implements FoodFactory {

    @Override
    public Food makeFood(String name) {
        if (name.equals("A")) {
            return new AmericanFoodA();
        } else if (name.equals("B")) {
            return new AmericanFoodB();
        } else {
            return null;
        }
    }
}
```



### 抽象工厂(Abstract Factory)

> 抽象工厂模式创建的是对象家族，也就是很多对象而不是一个对象，并且这些对象是相关的，也就是说必须一起创建出来。而工厂方法模式只是用于创建一个对象，这和抽象工厂模式有很大不同。

**适用场景**

1. 如果希望一个系统独立于它的产品的创建，组合和表示的时候，换句话说，希望一个系统只是知道产品的接口，而不关心实现的时候；
1. 如果一个系统要由多个产品系列中的一个来配置的时候，换句话说，就是可以动态的切换产品簇的时候；
1. 如果要强调一系列相关产品的接口，以便联合使用它们的时候。

**优点**

1. 分离接口和实现；
2. 使得切换产品簇变得容易。

**缺点**

1. 抽象工厂添加新的产品，所有具体工厂都需要添加，违反开闭原则（一种方法是仅实现一个方法，根据参数再判断具体实现，这种方法不安全，因为返回的参数必须是所有产品的父类）；
2. 容易造成类层次复杂。

**代码示例**

```java
abstract class Monitor {}

class LGMonitor extends Monitor{}

class SamsungMonitor extends Monitor{}

abstract class Mainframe {}

class AsusMainframe extends Mainframe{}

class HpMainframe extends Mainframe{}

/**
 * 工厂生产电脑需要主机和显示器，组合了两个工厂方法，形成抽象工厂
 */
abstract class AbstractComputerFactory {
    abstract Monitor createMonitor();
    abstract Mainframe createMainframe();
}

class ComputerFactory1 extends AbstractComputerFactory {

    @Override
    Monitor createMonitor() {
        return new LGMonitor();
    }

    @Override
    Mainframe createMainframe() {
        return new AsusMainframe();
    }
}

class ComputerFactory2 extends AbstractComputerFactory {

    @Override
    Monitor createMonitor() {
        return new SamsungMonitor();
    }

    @Override
    Mainframe createMainframe() {
        return new HpMainframe();
    }
}
```

### 单例模式(Singleton pattern)

> 确保一个类只有一个实例，并提供该实例的全局访问点;
>
> 使用一个私有构造函数、一个私有静态变量以及一个公有静态函数来实现，私有构造函数保证了不能通过构造函数来创建对象实例，只能通过公有静态函数返回唯一的私有静态变量。

**六种实现方式**

![单例模式比较](D:\Documents\坚果云\学习\博客\编程能力\设计模式\单例模式比较.png)

#### 懒汉式-线程不安全

延迟实例化，但是多线程环境下是不安全的，可能会多次实例化。

```java
public class Singleton {

    private static Singleton uniqueInstance;

    private Singleton() {}

    public static Singleton getUniqueInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}
```

#### 懒汉式-线程安全

对获取实例的方法加锁，可以避免多次实例化，保证线程安全，但是由于锁的等待，会损耗性能。

```java
public class Singleton {

    private static Singleton uniqueInstance;

    private Singleton() {}

	public static synchronized Singleton getUniqueInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
	}
}
```

#### 双重校验锁-线程安全

uniqueInstance 只需要被实例化一次，之后就可以直接使用了。加锁操作只需要对实例化那部分的代码进行，只有当 uniqueInstance 没有被实例化时，才需要进行加锁。

双重校验锁先判断 uniqueInstance 是否已经被实例化，如果没有被实例化，那么才对实例化语句进行加锁。

```java
public class Singleton {

    private volatile static Singleton uniqueInstance;

    private Singleton() {
    }

    public static Singleton getUniqueInstance() {
        if (uniqueInstance == null) {
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```

考虑下面的实现，也就是只使用了一个 if 语句。在 uniqueInstance == null 的情况下，如果两个线程同时执行 if 语句，那么两个线程就会同时进入 if 语句块内。虽然在 if 语句块内有加锁操作，但是两个线程都会执行 `uniqueInstance = new Singleton();` 这条语句，只是先后的问题，那么就会进行两次实例化，从而产生了两个实例。因此必须使用双重校验锁，也就是需要使用两个 if 语句。

```java
if (uniqueInstance == null) {
    synchronized (Singleton.class) {
        uniqueInstance = new Singleton();
    }
}
```

uniqueInstance 采用 volatile 关键字修饰也是很有必要的。`uniqueInstance = new Singleton();` 这段代码其实是分为三步执行。

1. 分配内存空间
2. 初始化对象
3. 将 uniqueInstance 指向分配的内存地址

但是由于 JVM 具有指令重排的特性，有可能执行顺序变为了 1>3>2，这在单线程情况下自然是没有问题。但如果是多线程下，有可能获得是一个还没有被初始化的实例，以致于程序出错。

使用 volatile 可以禁止 JVM 的指令重排，保证在多线程环境下也能正常运行。

#### 静态内部类实现

当 Singleton 类加载时，静态内部类 SingletonHolder 没有被加载进内存。只有当调用 `getUniqueInstance()` 方法从而触发 `SingletonHolder.INSTANCE` 时 SingletonHolder 才会被加载，此时初始化 INSTANCE 实例。

这种方式不仅具有延迟初始化的好处，而且SingletonHolder类是由JVM加载的，只会加载一遍，由虚拟机提供了对线程安全的支持。

```java
public class Singleton {

    private Singleton() {}

    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getUniqueInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

#### 饿汉式-线程安全

直接初始化静态属性，线程安全，但是直接实例化的方式也丢失了延迟实例化带来的节约资源的好处。

```java
public class Singleton {

    private static Singleton uniqueInstance = new Singleton();

    private Singleton() {}

    public static Singleton getUniqueInstance() {
        return uniqueInstance;
    }
}

```

#### 枚举实现

这是单例模式的最佳实践，它实现简单，并且在面对复杂的序列化或者反射攻击的时候，能够防止实例化多次。

```java
public enum Singleton {
    uniqueInstance;
}
```

如果`Singleton`需要`implements Serializable`，那么就可以通过setAccessible() 方法可以将私有构造函数的访问级别设置为 public，然后调用构造函数从而实例化对象，如果要防止这种攻击，需要在构造函数中添加防止实例化第二个对象的代码。

### 建造者模式

### 原型模式



## 结构型模式

### 外观(Facade)

> 它提供了一个统一的接口，用来访问子系统中的一群接口，从而让子系统更容易使用。
>
> 这种模式涉及到一个单一的类，该类提供了客户端请求的简化方法和对现有系统类方法的委托调用。

```java
public interface Shape {
   void draw();
}

class Rectangle implements Shape {
 
   @Override
   public void draw() {
      System.out.println("Rectangle::draw()");
   }
}

class Square implements Shape {
 
   @Override
   public void draw() {
      System.out.println("Square::draw()");
   }
}

class Circle implements Shape {
 
   @Override
   public void draw() {
      System.out.println("Circle::draw()");
   }
}
```

```java
public class ShapeMaker {
   private Shape circle;
   private Shape rectangle;
   private Shape square;
 
   public ShapeMaker() {
      circle = new Circle();
      rectangle = new Rectangle();
      square = new Square();
   }
 
   public void drawCircle(){
      circle.draw();
   }
   public void drawRectangle(){
      rectangle.draw();
   }
   public void drawSquare(){
      square.draw();
   }
}
```

```java
public class FacadePattern {
   public static void main(String[] args) {
      ShapeMaker shapeMaker = new ShapeMaker();
 
      shapeMaker.drawCircle();
      shapeMaker.drawRectangle();
      shapeMaker.drawSquare();      
   }
}
```

### 适配器(Adapter)

> 适配器模式(Adapter pattern): 将一个类的接口, 转换成客户期望的另一个接口。 适配器让原本接口不兼容的类可以合作无间。 对象适配器使用组合, 类适配器使用多重继承。例如typec转usb转接口。

## 行为型模式

### 责任链(Chain Of Responsibility)
