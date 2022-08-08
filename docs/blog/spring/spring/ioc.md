> 本文转载自 [Java全栈知识体系 https://pdai.tech/md/spring/spring-x-framework-ioc.html](https://pdai.tech/md/spring/spring-x-framework-ioc.html)

## 什么是控制反转和依赖注入

**控制反转**和**依赖注入**是 Spring 框架的核心功能。

**控制反转**：

> Ioc—Inversion of Control，即“控制反转”，**不是什么技术，而是一种设计思想**。在Java开发中，Ioc意味着将你设计好的对象交给容器控制，而不是传统的在你的对象内部直接控制。

**依赖注入**：

> 容器全权负责组件的装配，它会把符合依赖关系的对象通过属性或者构造函数传递给需要的对象。
>
> 符合依赖倒置原则，高层模块不应该依赖低层模块，两者都应该依赖其抽象。

**控制反转**是一种思想，而**依赖注入**是一种**设计模式**，依赖注入是实现控制反转的一种方式，但是控制反转还有其他实现方式，比如 ServiceLocator。

**控制反转**和**依赖注入**的过程：

- 对象仅通过构造函数参数、工厂方法的参数或在对象实例被构造或从工厂方法返回后设置的属性来定义它们的依赖关系（即与它们一起工作的其他对象）。

- 然后容器在创建 bean 时注入这些依赖项。这个过程基本上是 bean 本身通过使用类的直接构造或诸如服务定位器模式之类的机制来控制其依赖关系的实例化或位置的逆过程（因此称为控制反转）。

## IOC 的配置方式

### Xml 配置

顾名思义，就是将bean的信息配置在 xml 文件里，通过Spring加载文件为我们创建bean。这种方式出现很多早前的SSM项目中，将第三方类库或者一些配置工具类都以这种方式进行配置，主要原因是由于第三方类不支持Spring注解。

- **优点**： 可以使用于任何场景，结构清晰，通俗易懂
- **缺点**： 配置繁琐，不易维护，枯燥无味，扩展性差

**举例**：

1. 配置 xx.xml 文件
2. 声明命名空间和配置 bean

```xml
<bean id="userService" class="tech.pdai.springframework.service.UserServiceImpl">
   <property name="userDao" ref="userDao"/>
</bean>
```

### Java 配置

将类的创建交给我们配置的JavcConfig类来完成，Spring只负责维护和管理，采用纯Java创建方式。其本质上就是把在XML上的配置声明转移到Java配置类中

- **优点**：适用于任何场景，配置方便，因为是纯Java代码，扩展性高，十分灵活
- **缺点**：由于是采用Java类的方式，声明不明显，如果大量配置，可读性比较差

**举例**：

1. 创建一个配置类， 添加`@Configuration`注解声明为配置类
2. 创建方法，方法上加上`@Bean`，该方法用于创建实例并返回，该实例创建后会交给spring管理，方法名建议与实例名相同（首字母小写）。注：实例类不需要加任何注解

```java
@Configuration
public class BeansConfig {

    /**
     * 注册名称为 userDao 的 Bean ”UserDaoImpl“
     */
    @Bean("userDao")
    public UserDaoImpl userDao() {
        return new UserDaoImpl();
    }

    /**
     * 注册名称为 userService 的 Bean ”UserServiceImpl“
     */
    @Bean("userService")
    public UserServiceImpl userService() {
        UserServiceImpl userService = new UserServiceImpl();
        userService.setUserDao(userDao());
        return userService;
    }
}
```

### 注解配置

通过在类上加注解的方式，来声明一个类交给Spring管理，Spring会自动扫描带有@Component，@Controller，@Service，@Repository这四个注解的类，然后帮我们创建并管理，前提是需要先配置Spring的注解扫描器。

- **优点**：开发便捷，通俗易懂，方便维护。
- **缺点**：具有局限性，对于一些第三方资源，无法添加注解。只能采用XML或JavaConfig的方式配置

**举例**：

1. 对类添加 `@Component` 相关的注解，比如 `@Controller`，@Service，`@Repository`
2. 设置 `ComponentScan` 的 basePackage:
   1. `<context:component-scan base-package='tech.pdai.springframework'>`；
   2. 或者`@ComponentScan("tech.pdai.springframework")`注解；
   3. 或者 `new AnnotationConfigApplicationContext("tech.pdai.springframework")`指定扫描的 basePackage。

```java
@Service
public class UserServiceImpl {

    /**
     * 注入 UserDaoImpl
     */
    @Autowired
    private UserDaoImpl userDao;
    
    public List<User> findUserList() {
        return userDao.findUserList();
    }
}
```

## 依赖注入的三种方式

### 构造方法注入

1. **在XML配置方式中**，`<constructor-arg>`是通过构造函数参数注入，比如下面的 xml:

```xml
<bean id="userService" class="tech.pdai.springframework.service.UserServiceImpl">
    <constructor-arg name="userDao" ref="userDao"/>
</bean>
```

本质上是new UserServiceImpl(userDao)创建对象, 所以对应的service类是这样的：

```java
public class UserServiceImpl {

    private final UserDaoImpl userDao;

    // 构造方法参数和 constructor-arg 对应上
    public UserServiceImpl(UserDaoImpl userDaoImpl) {
        this.userDao = userDaoImpl;
    }

    public List<User> findUserList() {
        return this.userDao.findUserList();
    }

}
```

2. **在注解和Java配置方式下**（推荐方式）

```java
// 添加 Service 注解，表明该类交由 Spring 容器管理
@Service
public class UserServiceImpl {

    private final UserDaoImpl userDao;

	// 表示通过构造方法注入
    @Autowired // 这里@Autowired也可以省略
    public UserServiceImpl(final UserDaoImpl userDaoImpl) {
        this.userDao = userDaoImpl;
    }

    public List<User> findUserList() {
        return this.userDao.findUserList();
    }

}

```

### Setter 方法注入

1. **在XML配置方式中**，property 都是 setter 方式注入，比如下面的 xml:

```xml
<bean id="userService" class="tech.pdai.springframework.service.UserServiceImpl">
    <property name="userDao" ref="userDao"/>
</bean>
```

>  本质上包含两步：
>  1. 第一步，需要new UserServiceImpl()创建对象, 所以需要默认构造函数
>  2. 第二步，调用setUserDao()函数注入userDao的值, 所以需要setUserDao()函数

所以对应的service类是这样的：

```java
public class UserServiceImpl {

    private UserDaoImpl userDao;

    public UserServiceImpl() {}

    // 需要有 Setter 方法
    public void setUserDao(UserDaoImpl userDao) {
        this.userDao = userDao;
    }
}

```

2. **在注解和Java配置方式下**

```java
public class UserServiceImpl {

    private UserDaoImpl userDao;

    // 通过注解指定 setter 方法
    @Autowired
    public void setUserDao(UserDaoImpl userDao) {
        this.userDao = userDao;
    }
}

```

### 注解注入

以@Autowired（自动注入）注解注入为例，修饰符有三个属性：Constructor，byType，byName。默认按照byType注入。

- **constructor**：通过构造方法进行自动注入，spring会匹配与构造方法参数类型一致的bean进行注入，如果有一个多参数的构造方法，一个只有一个参数的构造方法，在容器中查找到多个匹配多参数构造方法的bean，那么spring会优先将bean注入到多参数的构造方法中。
- **byName**：被注入bean的id名必须与set方法后半截匹配，并且id名称的第一个单词首字母必须小写，这一点与手动set注入有点不同。
- **byType**：查找所有的set方法，将符合符合参数类型的bean注入。

示例：

```java
@Service
public class UserServiceImpl {

    // 通过在属性中添加注解注入
    @Autowired
    private UserDaoImpl userDao;

}
```

### 为什么推荐构造器注入方式？

推荐使用构造器注入的方式，这种方式**能够保证注入的组件不可变，并且确保需要的依赖不为空**。此外，构造器注入的依赖总是能够在返回客户端（组件）代码的时候保证完全初始化的状态，即：

- **依赖不可变**：其实说的就是final关键字。
- **依赖不为空**（省去了我们对其检查）：当要实例化 UserServiceImpl 的时候，由于自己实现了有参数的构造函数，所以不会调用默认构造函数，那么就需要 Spring 容器传入所需要的参数，所以就两种情况：1、有该类型的参数->传入，OK 。2：无该类型的参数->报错。
- **完全初始化的状态**：这个可以跟上面的依赖不为空结合起来，向构造器传参之前，要确保注入的内容不为空，那么肯定要调用依赖组件的构造方法完成实例化。而在 Java 类加载实例化的过程中，构造方法是最后一步（之前如果有父类先初始化父类，然后自己的成员变量，最后才是构造方法），所以返回来的都是初始化之后的状态。

所以通常是这样的：

```java
@Service
public class UserServiceImpl {

    // 属性设置为 final，可以提高性能
    private final UserDaoImpl userDao;

    // 使用构造器注入，且参数设置为 final
    public UserServiceImpl(final UserDaoImpl userDaoImpl) {
        this.userDao = userDaoImpl;
    }

}
```

如果使用 setter 注入，缺点显而易见，对于 IOC 容器以外的环境，除了使用反射来提供它需要的依赖之外，**无法复用该实现类**。而且将一直是个潜在的隐患，因为你不调用将一直无法发现 `NullPointerException` 的存在。

```java
// 这里只是模拟一下，正常来说我们只会暴露接口给客户端，不会暴露实现。
UserServiceImpl userService = new UserServiceImpl();
userService.findUserList(); // -> NullPointerException, 潜在的隐患
```

**循环依赖的问题**：使用 field 注入可能会导致循环依赖，即 A 里面注入B，B 里面又注入 A：

如果使用构造器注入，在 spring 项目启动的时候，就会抛出：BeanCurrentlyInCreationException：Requested bean is currently in creation: Is there an unresolvable circular reference？从而提醒你避免循环依赖，如果是 field 注入的话，启动的时候不会报错，在使用那个 bean 的时候才会报错。

