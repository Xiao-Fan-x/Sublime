http://hollischuang.gitee.io/tobetopjavaer/#/

多态分类：

（动态多态）

特设多态：函数重载

参数多态：泛型

子类型：父类的引用指向子类的对象

继承、组合、代理

```java
public class Test {
    public static void main(String[] args) {
        UserDao target = new UserDao();
        UserDaoProxy proxy = new UserDaoProxy(target);
        proxy.save();
    }
}

interface IUserDao{
    void save();
}

class UserDao implements IUserDao{
    @Override
    public void save() {
        System.out.println("------已保存数据----");
    }
}

class UserDaoProxy implements IUserDao{
    private IUserDao target;
    public UserDaoProxy(IUserDao target){
        this.target = target;
    }

    @Override
    public void save() {
        System.out.println("开始事务...");
        target.save();//执行目标对象的方法
        System.out.println("提交事务...");
    }
}
```

（静态多态）

重载和重写这两个概念：

1、重载是一个编译期概念、重写是一个运行期概念。

2、重载遵循所谓“编译期绑定”，即在编译时根据参数变量的类型判断应该调用哪个方法。

3、重写遵循所谓“运行期绑定”，即在运行的时候，根据引用变量所指向的实际对象的类型来调用方法。

4、Java中的方法重写是Java多态（子类型）的实现方式。而Java中的方法重写其实是特设多态的一种实现方式。

重载：指的是在同一个类中，多个函数或者方法有同样的名称，但是参数列表不相同的情形，这样的同名不同参数的函数或者方法之间，互相称之为重载函数或者方法。

1、被重载的方法必须改变参数列表； 2、被重载的方法可以改变返回类型； 3、被重载的方法可以改变访问修饰符； 4、被重载的方法可以声明新的或更广的检查异常； 5、方法能够在同一个类中或者在一个子类中被重载。

重写：指的是在Java的子类与父类中有两个名称、参数列表都相同的方法的情况。由于他们具有相同的方法签名，所以子类中的新方法将覆盖父类中原有的方法。

1、参数列表必须完全与被重写方法的相同； 2、返回类型必须完全与被重写方法的返回类型相同； 3、访问级别的限制性一定不能比被重写方法的强； 4、访问级别的限制性可以比被重写方法的弱；
5、重写方法一定不能抛出新的检查异常或比被重写的方法声明的检查异常更广泛的检查异常 6、重写的方法能够抛出更少或更有限的异常（也就是说，被重写的方法声明了异常，但重写的方法可以什么也不声明） 7、不能重写被标示为final的方法；
8、如果不能继承一个方法，则不能重写这个方法。

继承的根本原因是因为要*复用*，而实现的根本原因是需要定义一个*标准*

## 三目运算：

```
Map<String,Boolean> map =  new HashMap<String, Boolean>();
Boolean b = (map!=null ? map.get("Hollis") : false);
```

**因为以上代码，在小于JDK 1.8的版本中执行的结果是NPE，在JDK 1.8 及以后的版本中执行结果是null。**

JLS 15中对条件表达式（三目运算符）做了细分之后分为三种，区分方式：

> 如果表达式的第二个和第三个操作数都是布尔表达式，那么该条件表达式就是布尔表达式
>
> 如果表达式的第二个和第三个操作数都是数字型表达式，那么该条件表达式就是数字型表达式
>
> 除了以上两种以外的表达式就是引用表达式

又跟据JLS15.25.3中规定：

> 如果引用条件表达式出现在赋值上下文或调用上下文中，那么条件表达式就是合成表达式

```
Boolean b = maps == null ? Boolean.valueOf(false) : (Boolean)maps.get("Hollis");
```

但是在Java 7中可没有这些规定（Java 8之前的类型推断功能还很弱），编译器只知道表达式的第二位和第三位分别是基本类型和包装类型，而无法推断最终表达式类型。

```
Boolean b = Boolean.valueOf(maps == null ? false : ((Boolean)maps.get("Hollis")).booleanValue());
```

所以，相比Java 8中多了一步自动拆箱，所以会导致NPE。

其中的 Javadoc 详细的说明了缓存支持 -128 到 127 之间的自动装箱过程。最大值 127 可以通过 `-XX:AutoBoxCacheMax=size` 修改。

实际上这个功能在 Java 5 中引入的时候,范围是固定的 -128 至 +127。后来在 Java 6 中，可以通过 `java.lang.Integer.IntegerCache.high` 设置最大值。

缺点：

包装对象的数值比较，不能简单的使用 `==`，虽然 -128 到 127 之间的数字可以，但是这个范围之外还是需要使用 `equals` 比较。

前面提到，有些场景会进行自动拆装箱，同时也说过，由于自动拆箱，如果包装类对象为 null ，那么自动拆箱时就有可能抛出 NPE。

如果一个 for 循环中有大量拆装箱操作，会浪费很多资源。

## StringBuilder<StringBuffer<concat<+<StringUtils.join

StringBuffer在StringBuilder的基础上，做了同步处理，所以在耗时上会相对多一些。

StringUtils.join也是使用了StringBuilder，并且其中还是有很多其他操作，所以耗时较长，这个也容易理解。其实StringUtils.join更擅长处理字符串数组或者列表的拼接。

## 字符串常量池的位置

在JDK 7以前的版本中，字符串常量池是放在永久代中的。

因为按照计划，JDK会在后续的版本中通过元空间来代替永久代，所以首先在JDK 7中，将字符串常量池先从永久代中移出，暂时放到了堆内存中。

在JDK 8中，彻底移除了永久代，使用元空间替代了永久代，于是字符串常量池再次从堆内存移动到永久代中

## 常量池

在Java体系中，共用三种常量池。分别是**字符串常量池**、**Class常量池**和**运行时常量池**。

常量池中主要存放两大类常量：字面量（literal）和符号引用（symbolic references）

根据Java虚拟机规范约定：每一个运行时常量池都在Java虚拟机的方法区中分配，在加载类和接口到虚拟机后，就创建对应的运行时常量池。

## intern的功能很简单：

在每次赋值的时候使用 String 的 intern 方法，如果常量池中有相同值，就会重复使用该对象，返回对象引用。

Set类

1、TreeSet 是二叉树实现的，TreeSet中的数据是自动排好序的，不允许放入 null值 2、HashSet 是哈希表实现的，HashSet中的数据是无序的，可以放入
null值，但只能放入一个null，两者中的值都不能重复，就如数据库中的唯一约束

## SynchronizedList和Vector的区别

1.Vector使用同步方法实现，synchronizedList使用同步代码块实现。

2.两者的扩充数组容量方式不一样（两者的add方法在扩容方面的差别也就是ArrayList和Vector的差别。

SynchronizedList和Vector的区别目前为止有两点： 1.如果使用add方法，那么他们的扩容机制不一样。 2.SynchronizedList可以指定锁定的对象。

**但是**SynchronizedList中实现的类并没有都使用synchronized同步代码块。其中有listIterator和listIterator(int index)并没有做同步处理。但是Vector却对该方法加了方法锁。
所以说，在使用SynchronizedList进行遍历的时候要手动加锁。

**总结**

1.SynchronizedList有很好的扩展和兼容功能。他可以将所有的List的子类转成线程安全的类。 2.使用SynchronizedList的时候，进行遍历时要手动进行同步处理。
3.SynchronizedList可以指定锁定的对象。

**同步代码块和同步方法的区别**

1.同步代码块在锁定的范围上可能比同步方法要小，一般来说锁的范围大小和性能是成反比的。

2.同步块可以更加精确的控制锁的作用域（锁的作用域就是从锁被获取到其被释放的时间），同步方法的锁的作用域就是整个方法。

3.同步代码块可以选择对哪个对象加锁，但是静态方法只能给this对象加锁。

## HashMap中hash方法的原理

直接定址法：直接以关键字k或者k加上某个常数（k+c）作为哈希地址。

数字分析法：提取关键字中取值比较均匀的数字作为哈希地址。

除留余数法：用关键字k除以某个不大于哈希表长度m的数p，将所得余数作为哈希表地址。

分段叠加法：按照哈希表地址位数将关键字分成位数相等的几部分，其中最后一部分可以比较短。然后将这几部分相加，舍弃最高进位后的结果就是该关键字的哈希地址。

平方取中法：如果关键字各个部分分布都不均匀的话，可以先求出它的平方值，然后按照需求取中间的几位作为哈希地址。

伪随机数法：采用一个伪随机数当作哈希函数。

解决哈希碰撞：

- 开放定址法：
    - 开放定址法就是一旦发生了冲突，就去寻找下一个空的散列地址，只要散列表足够大，空的散列地址总能找到，并将记录存入。
- 链地址法
    - 将哈希表的每个单元作为链表的头结点，所有哈希地址为i的元素构成一个同义词链表。即发生冲突时就把该关键字链在以该单元为头结点的链表的尾部。
- 再哈希法
    - 当哈希地址发生冲突用其他的函数计算另一个哈希函数地址，直到冲突不再产生为止。
- 建立公共溢出区
    - 将哈希表分为基本表和溢出表两部分，发生冲突的元素都放入溢出表中。

## Stream有以下特性及优点：

- 无存储。Stream不是一种数据结构，它只是某种数据源的一个视图，数据源可以是一个数组，Java容器或I/O channel等。
- 为函数式编程而生。对Stream的任何修改都不会修改背后的数据源，比如对Stream执行过滤操作并不会删除被过滤的元素，而是会产生一个不包含被过滤元素的新Stream。
- 惰式执行。Stream上的操作并不会立即执行，只有等到用户真正需要结果的时候才会执行。
- 可消费性。Stream只能被“消费”一次，一旦遍历过就会失效，就像容器的迭代器那样，想要再次遍历必须重新生成。

Stream s = strings.stream().filter(string -> string.length()<= 6)

.map(String::length.sorted().limit(3).distinct();

**filter**

filter 方法用于通过设置的条件过滤出元素

**map**

map 方法用于映射每个元素到对应的结果

**distinct**

distinct主要用来去重

**limit/skip**

limit 返回 Stream 的前面 n 个元素；skip 则是扔掉前 n 个元素。

**forEach**

Stream 提供了方法 'forEach' 来迭代流中的每个数据。

**count**

count用来统计流中的元素个数。

**collect**

collect就是一个归约操作，可以接受各种做法作为参数，将流中的元素累积成一个汇总结果

asList 得到的只是一个 Arrays 的内部类，一个原来数组的视图 List，因此如果对它进行增删操作会报错

用 ArrayList 的构造器可以将其转变成真正的 ArrayList

//Iterator遍历 Iterator it = list.iterator(); while (it.hasNext()) { System.out.println(it.next()); }

//Stream 遍历 list.forEach(System.out::println);

list.stream().forEach(System.out::println);

## ConcurrentSkipListMap 和 ConcurrentHashMap 的主要区别：

a.底层实现方式不同。ConcurrentSkipListMap底层基于跳表。ConcurrentHashMap底层基于Hash桶和红黑树。

b.ConcurrentHashMap不支持排序。ConcurrentSkipListMap支持排序。

## 输出

PrintWriter pw = new PrintWriter(System.out, true);

## 动态代理：

JDK动态代理和Cglib动态代理的区别

JDK的动态代理有一个限制，就是使用动态代理的对象必须实现一个或多个接口。如果想代理没有实现接口的类，就可以使用CGLIB实现。

Cglib是一个强大的高性能的代码生成包，它可以在运行期扩展Java类与实现Java接口。它广泛的被许多AOP的框架使用，例如Spring AOP和dynaop，为他们提供方法的interception（拦截）。

Cglib包的底层是通过使用一个小而快的字节码处理框架ASM，来转换字节码并生成新的类。不鼓励直接使用ASM，因为它需要你对JVM内部结构包括class文件的格式和指令集都很熟悉。

Cglib与动态代理最大的区别就是：

使用动态代理的对象必须实现一个或多个接口

使用cglib代理的对象则无需实现接口，达到代理类无侵入。

# Java 集合框架

```java
@SafeVarargs
public static <T> List<T> asList(T... a)

Integer[] arr = {1, 2, 3};
List list = Arrays.asList(arr);
```

应该注意的是 asList() 的参数为泛型的变长参数，不能使用基本类型数组作为参数，只能使用相应的包装类型数组。

Collection 继承了 Iterable 接口，其中的 iterator() 方法能够产生一个 Iterator 对象，通过这个对象就可以迭代遍历 Collection 中的元素。

## 得到一个线程安全的 ArrayList。

```java
List<String> list = new ArrayList<>();
List<String> synList = Collections.synchronizedList(list);
```

也可以使用 concurrent 并发包下的 CopyOnWriteArrayList 类。

```java
List<String> list = new CopyOnWriteArrayList<>();
```

但是 CopyOnWriteArrayList 有其缺陷：

- 内存占用：在写操作时需要复制一个新的数组，使得内存占用为原来的两倍左右；
- 数据不一致：读操作不能读取实时性的数据，因为部分写操作的数据还未同步到读数组中。

所以 CopyOnWriteArrayList 不适合内存敏感以及对实时性要求很高的场景

#  

# JVM

是不是所有的对象和数组都会在堆内存分配空间？

不一定，随着JIT编译器的发展，在编译期间，如果JIT经过逃逸分析，发现有些对象没有逃逸出方法，那么有可能堆内存分配会被优化成栈内存分配。但是这也并不是绝对的。就像我们前面看到的一样，在开启逃逸分析之后，也并不是所有User对象都没有在堆上分配。

## 类加载器

Java中提供的这四种类型的加载器，是有各自的职责的：

- Bootstrap ClassLoader ，主要负责加载Java核心类库，%JRE_HOME%\lib下的rt.jar、resources.jar、charsets.jar和class等。
- Extention ClassLoader，主要负责加载目录%JRE_HOME%\lib\ext目录下的jar包和class文件。
- Application ClassLoader ，主要负责加载当前应用的classpath下的所有类
- User ClassLoader ， 用户自定义的类加载器,可加载指定路径的class文件

也就是说，一个用户自定义的类，如com.hollis.ClassHollis 是无论如何也不会被Bootstrap和Extention加载器加载的

#### 好处：

可以避免类的重复加载

保证了安全性

### 关系：

类加载器之间的父子关系一般不会以继承（Inheritance）的关系来实现，而是都使用组合（Composition）关系来复用父加载器的代码的

# JVM内存结构、 Java内存模型 以及 Java对象模型 

