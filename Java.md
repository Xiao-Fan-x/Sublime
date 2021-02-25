# java

## this

 this三类结构的描述：

- 当前类中的属性：this属性；

- 当前类中的方法（普通方法、构造方法）：this（），this。方法名称（）；

- 描述当前对象；


如何评价一个代码的好坏： 代码的结构可以重用，提供的是一个中间独立的支持； 我们的目标是没有重复

对于本类构造方法的互相调用需要注意以下几点重要问题 - 构造方法必须在实例化新对象的时候调用，所以this()的语句只允许放在构造方法的首行； -
构造方法互相调用是请保留有程序的出口

类名称一定要有意义，可以明确的描述某一类事物； 类之中的所有属性都必须使用private进行封装，同时封装的属性必须要提供有setter、getter方法
类之中可以提供有无数多个构造方法，但是必须要保留有无参构造方法； 类之中不允许出现任何的输出语句，所有内容的获取必须返回
【非必须】可以提供有一个获取对象详细信息的方法，暂时将此方法名称定义为getinfo()


## static 可以在没有实例化对象的情况下进行调用 最好有最上层类进项调用修改

static方法、非static方法，这两个方法之间在调用上就有了限制 - static方法只允许调用static属性或static方法； -
非static方法允许调用static属性或static方法； 所有的static定义的属性和方法都可以在没有实例化对象的前提下使用，
而所有的非static定义的属性和方法必须要有实例化对象的情况下才可以使用

static定义的方法或是属性都不是代码编写之初所需要的考虑的内容，
只有在回避实例化对象调用并且描述公共属性的情况下才会考虑使用static定义的方法或是属性


## 代码块

在程序中使用{}定义的结构就成为代码块，而后根据代码块出现的位置以及定义的关键字的不通话，代码块可以分为：普通代码块、构造块、静态块、同步代码块，其中对于同步代码块是在多线程的时候才会讲解到

普通代码块：可以在一个方法中进行一些结构的拆分，以防止相同变量名称所带来的的互相影响
构造块：构造块会优先于构造方法执行，并且每一次实例化新对象的时候都会调用构造块中的代码
静态块：主要指的是使用static关键字定义的代码块，静态块的定义需要考虑到 两种情况：主类中定义静态块、非主类中定义静态块

静态代码块会优先于构造块执行，并且不管有多少个实例对象出现静态代码块只会执行一次，主要目的是为类中的静态属性初始化

对于静态代码块还必须考虑另外一种情况，在主类中定义的形式 在主类中进行静态代码块的定义

同步代码块

## 数组

如果发现类中没有属性存在的意义，那么定义的方法就没有必要使用普通方法了，因为普通方法需要在有实例化对象产生的情况下才可以调用。

### 数组相关类库 数组.sort() 数组排序 System.arraycopy(数组，源数组开始点，目标数组，目标数组开始点，拷贝长度)

### 可变参数 类型 + ... + 名称 


## 字符串与字节 
public String(char[] value)		|构造|	传入的全部字符数组变为字符串 
public String(char[] value,int offset,int count)  |构造|		将部分字符数组变为字符串	 public char charAt(int index)	|普通| 	获取指定索引位置的字符	 
public char[] toCharArray() 	|普通|	将字符串中的数据以字符数组的形式返回
public String(byte[] bytes) 	构造  	将全部的字节数组变为字符 
public String(byte[] bytes,int offset,int length) 	构造 	将部分字节数组变为字符串 public byte[] getBytes() 	普通 	将字符串转为字节数组
public byte[] getBytes(String charsetName) throws UnsupportedEncodingException
 普通 	编码转换	


## 字符串比较
public boolean equals(String anObject) 	|普通| 	区分大小写的相等判断 
public boolean equalsIgnoreCase(String anotherString)  |普通| 	不区分大小写比较 
public int compareTo(String anotherString) |普通| 进行字符串大小比较，该方法返回一个int数据，该数据有三种取值：大于(>0)、小于(<0)、等于(=0) public int compareToIgnoreCase(String anotherString) |普通| 	不区分大小写进行字符串大小比较

## 字符串查找
public boolean contains(String s) 	|普通| 	判断子字符串是否存在 
public int indexOf(String str) 	|普通| 	从头查找指定字符串的位置，找不到返回 -1 
public int indexOf(String str,int fromIndex) |普通| 	从指定位置查找指定字符串的位置 
public int lastIndexOf(String str) |普通|  由后向前查找指定字符串的位置 
public int lastIndexOf(String str,int fromIndex)   |普通|从指定位置由后向前查找指定字符串的位置 
public boolean startsWith(String prefix)  |普通|  判断是否以指定字符串开头
public Boolean startsWith(String prefix,int toffset)  |普通|  指定位置判断是否以指定的字符串开头
public boolean endsWith(String suffix)  |普通|  	判断是否以指定字符串结尾

## 字符串替换 
public String replaceAll(String regex,String replacement) |普通|		全部替换
public String replaceFirst(String regex,String replacement) |普通|		替换第一个

## 字符串拆分
public String[] split(String regex) 	|普通| 	按照指定的字符串全部拆分 
public String[] split(String regex,int limit)	|普通|按照指定的字符串拆分为指定个数，后面不拆了

## 字符串截取
public String substring(int beginIndex)  	|普通| 	从指定索引截取到结尾
public String substring(int beginIndex,int endIndx) |普通| 	截取指定索引范围中的子字符串

## 字符串格式化
常用：字符串(%s)、字符(%c)、整数(%d)
public static String format(String format,各种类型...args) |普通| 	根据指定结构进行文本格式显示

## String其他方法
public String concat(String str) |普通| 描述的是字符串的连接过程
public String intern() 	|普通| 	字符串入池
public boolean isEmpty() |普通| 	判断是否为空字符串
* 此操作并没有进行静态的定义
在字符串定义的时候“""”和“null”不是一个概念，一个表示有实例化对象，一个表示没有实力虎啊对象，而isempty()
判断字符串的内容，
public int length()  || 	计算字符串的长度
public	String trim() 	||   去除左右的空格信息
public String toUpperCase() || 转大写
public String toLowerCase() || 转小写

Java之中String类已经提供有大量的方法了，但是缺少了一个首字母大写的方法

# 继承
私有操作属于隐式继承，不能直接访问，但可以间接访问
而非私有操作属于显式继承

## 重写
Overloading与Coerride的区别？ Overloading时返回参数是否相同？

overloading 			override
重载						覆写
方法名称相同，参数的类型及个数不同 	| 参数名称、参数类型及个数、返回值相同
没有权限限制	 	|	子类覆写方法不能拥有更严格的控制权限
发生在一个类中	|		发生在继承关系类中

在进行方法重载的时候并没有对返回类型做出限制，但是好的习惯应该保持返回类型的一致

## final 
不能被继承、不能覆写
final定义的常量赋值后不能修改
为了体现共享的概念，往往会使用一种全局常量形式
public static（共享的）final 
在定义全局常量的时候每一个字母必须大写表述


在方法的时候也可以使用final来定义参数，此时也表示一个常量的概念
（最为常见、最有用处）

## Annotation注解
annotation式从jdk1.5之后提出的一个新的开发技术，利用annotation可以有效减少程序配置的代码，annotation可以进行一些结构化的定义。annotation是以一种注解的形式实现的程序开发

程序开发的过程
过程一：在程序定义的时候将所有可能使用到的资源全部定义到代码之中；
- 如果此时服务器的相关的地址发生了改变，那么对于程序而言就需要进行源代码修改
过程二：引入配置文件，在配置文件之中定义全部要使用的服务器资源
- 在配置项不多的情况下，此类配置非常好用，并且十分简单。但是如果所有结构都是用这种办法开发，就可能出现一种可怕的场景：配置文件暴多；
- 所有的操作都需要通过配置文件完成，对于开发的难度提升了
过程三：将配置信息重新写回程序，利用一些特殊的标记与程序代码进行分离，这就是注解的作用，这也就是Annotation的基本依据
- 如果全部都使用注解开发，难度太高了，配置文件有好处也有坏处，所以现在人们的开发基本上围绕着配置文件以及注解的形式完成的。

# 向上转型
向上的主要特点在于，可以对参数进行同意的设计。但是为什么此时不使用重载来解决当前问题呢？
答：利用重载的确可以解决当前的设计，的确可以实现与之前完全一样的额效果。但是在进行程序类设计的时候除了满足于当付钱的要求之外，如果说现在醉着项目的发展，Message产生了3万个子类，每当扩充一个子类之后就要追加一个方法的重载。

向上转型：接受或返回参数的统一性，调用的方法是子类重写的方法
向上描述的式一些公共的特征，而向下描述的是子类自己特殊的定义环境，但是我们需要明确的是向下转型不是一件安全的事情。因为在进行向下转型之前要首先发生向上转型。


以后只要是发生对象的向下转型之前一定要首先发生向上转型，两个没有任何关系的实例如果要发生强制转换，那么就会出现“ClassCastException”异常，所以向下转型并不是一件安全的事情。

在以后进行一些完善性的程序开发的过程之中，对于转型之前一定要使用instanceof()判断。

在Java之中之有一个类是不存在有继承关系的，那么这个类就是Object，也就是说所有的类默认情况下都是Object类子类，以下两种类的定义效果完全相同

如果一个程序的方法要求可以接受所有类对象的时候就可以利用Object实现处理。
在Java设计的过程之中对于所有的引用数据类型实际上都可以使用Object类进行接受，包括数组也可以

# Object类
Object是一个万能的数据类型，它更加适合于进行程序的标准设计
Object类提供的方法：
public String toString() 

# 抽象类
抽象类的基本定义：主要作用在于对子类中覆写方法进行约定，在抽象类里面可以去定义一些方法，以实现这样的约定
1. 抽象类不能被实例化(初学者很容易犯的错)，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。

2. 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

3. 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现也就是方法的具体功能。

4. 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。

5. 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。
在定义抽象类的时候绝对不能够使用final关键字来进行定义，因为抽象类一定要有子类
抽象类中可以提供有static方法，并且该方法不受到抽象类对象的局限
即使抽象类没有实例化对象，那么也无法直接使用关键字new获取抽象类的对象，必须依靠子类完成
static方法永远不受到实例化对象或结构的限制，永远可以直接通过类名称进行调用

## 包装类 八种
Java中包装类一共提供有两种类型：
- 对象型包装类（Object）直接子类：Boolean，Character
- 数值型的包装类（Number直接子类）： Byte、Short、Integer、Long、Float、Double

public byte byteValue() 	||	从包装类中获取byte数据
public short shortValue()	||  从包装类中获取short数据
public abstract int intValue()	|| 
public abstract long longValue() ||	 
public abstract float floatValue()	||
public abstract double doubleValue() ||	

## 装箱与拆箱操作
基本数据类型的包装类都是为了基本数据类型转为对象提供的，
数据装箱
Integer类：public Integer(int value);
Double类：public Double(double value);
Boolean类：public Boolean(boolean value);
数据拆箱
数值型包装类已经由Number类定义了拆箱的方法了
Boolean型：public boolean booleanValue();

从JDK1.9之后，对于多有包装类之中提供的构造方法就变为了过期处理，不建议用户在继续使用了，这是因为从JDK1.5之后提供了自动的装箱与拆箱操作，所以这种手工的模式基本上没人用了。

观察自动装箱与拆箱
public class Test {
	public static void main(String[] args) {
		Integer obj = 10;//自动装箱，此时不再关心构造方法了 
		int num = obj;//自动拆箱
		obj++;//包装类对象可以直接参与数学运算
		System.out.println(num*obj);
	}
}
//110
除了提供数学运算支持之外，使用自动装箱最大的好处是可以实现Object接收基本数据类型的操作。
Object接收小数：
public class Test{
	public static void main(String args[]){
	Object obj = 19.2;//double自动装箱为Double，向上转型为Object
	double num = (Double)obj;//向下转型为包装类，再自动拆箱
	System.out.println(num*2);
  }
}
//38.4

JDK1.5之后提供的自动支持功能，到了JDK1.9之后为了巩固此概念，所以将包装类设为过期

# 接口
最原始的定义接口之中是只包含有抽象方法与全局常量的，但是从JDK1.8开始引入了Lambda表达式的概念，所以接口的定义也得到了加强，除了抽象方法与全局常量之外，还可以定义普通方法或静态方法。如果从设计本身的角度来将，接口之中的组成还是应该以抽象方法和全局常量为主。

为了区分出接口与类，接口名称前往往会加入“I”
接口的使用：
- 接口需要被子类实现（implements），一个子类可以实现多个接口；
- 子类（如果不是抽象类）那么一定要覆写接口之中的全部抽象方法；
- 接口对象可以利用子类对象的向上转型进行实例化。

子类实现多个接口，所以这个子类可以是这些接口任意一个接口的实例那么就表示作此时这些接口实例之间是可以转换的。

Object类对象可以接受所有数据类型，包括基本数据类型、类对象、接口对象，数组
由于接口描述的是一个公共的定义标准，所以在接口之中所有的抽象方法的访问权限都为public，写与不写都是一样的

接口可以省略abstract
虽然接口无法去继承一个父类，但是一个接口却可以通过extends继承若干个父接口，此时称为接口的多继承

接口的使用：
- 进行标准设置；
- 表示一种操作的能力；
- 暴露远程方法试图，这个一般都在RPC分布式开发中使用

从JDK1.8之后开始，为了解决接口设计的缺陷，所以在接口之中允许开发者定义普通方法

接口中的普通方法必须追加default的申明，但是需要提醒的是，该操作属于挽救功能，所以不是必须的话，不应该作为设计的首选

最好的方法，是在接口与实现类之间创建一个抽象方法（过度抽象类），用抽象类做出实现。
除了可以追加普通方法之外，接口里面也可以定义static方法，而static方法可以通过接口直接调用


## 代理设计模式（Proxy）


## 抽象类与接口区别

| 定义关键字 | abstract class 抽象类{} | interface |
| ---- | ---- |  
| 组成 |	构造、普通方法、静态方法、全局常量、普通成员、static方法 | 抽象方法、全局常量、普通方法、static方法
| 权限 | 可以使用各种权限 | 只能怪使用public
| 子类使用 | 子类通过extends关键字可以继承一个抽象类 | 子类使用impletments关键字可以实现多个接口
| 关系 | 抽象类可以实现若干接口 | 接口不允许继承抽象类，但是允许继承多个父接口
| 使用 | 1.抽象类或接口必须定义子类；2.子类一定要覆写抽象类或接口中的全部抽象方法；3.通过子类的向上转型实现抽象类或接口对象实例化

当抽象类和接口都可以使用的情况下优先要考虑接口，因为接口可以避免子类的单继承局限，另外从一个正常的设计角度而言，也需要先从接口来进行项目的整体设计。

# 泛型
JDK1.5之后提供泛型技术，而泛型的本质在于，类中的属性或方法的参数与返回类型可以由对象实例化的时候都动态决定

## 泛型通配符
< ? extends ...>
< ? super ...>

# 单例设计模式：主要是一种控制实例化对象产生个数的设计操作
类只允许提供有一个实例化对象，那么此时首先应该控制的就是构造方法。
在很多情况下有些类是不需要重复产生对象的。



| 重写与重载的区别 | 重载方法 | 重写方法                                       |
| ---------------- | -------- | ---------------------------------------------- |
| 参数列表         | 必须修改 | 一定不能修改                                   |
| 返回类型         | 可以修改 | 一定不能修改                                   |
| 异常             | 可以修改 | 可以减少或删除，一定不能抛出新的或者更广的异常 |
| 访问             | 可以修改 | 一定不能做更严格的限制（可以降低限制）         |

## 多例设计


# 枚举

JDK1.5之后才提出
主要作用是用于定义有限个数对象的一种结构（多例设计），枚举就属于多例设计，并且其结构要比多例设计更加简单

基本定义：从JDK1.5之后在程序之中提供有enum的关键字，利用此关键字可以实现枚举的定义



多例设计与枚举设计虽然可以实现相同的功能，但是使用枚举可以在程序编译的时候，判断所使用的实例化对象是否存在。

在进行枚举处理的时候还可以利用values（）方法获取所有的枚举对象进行输出

多例上是无法实现这种与switch直接连接的，多例要想实现就需要编写大量的if语句



Enum类

枚举不属于一种新的结构，他的本质相当于是一个类，但是这个类默认会继承Enum类

| 方法名称 | 构造 | 传入名字和序号
| protected Enum(String name,int ordinal) | 普通 | 获得对象名字
| public final String name() | 普通 | 获得对象名字
| public final int ordinal() | 普通 | 获得对象序号

enum与Enum的区别：
enum：是从JDK1.5之后提供的一个关键字，用于定义枚举类
Enum：是一个抽象类，所以使用后enum关键字定义的类就默认继承了此类

在枚举类里面可以直接定义抽象方法

# 异常

try捕捉的是异常实例化对象

Error：此时程序还未执行出现的错误，开发者无法处理
Exception：程序中出现的异常，开发者可以处理。

throw与throws区别：
throw：是在代码块中使用的，主要是手工进行异常对象的抛出
throws：是在方法定义上使用的，表示将此方法中可能产生的异常明确告诉给调用处，由调用出进行处理

RuntimeException与Exception区别：
RuntimeException是Exception的子类
RuntimeException标注的异常可以不需要进行强制性处理，而Exception异常必须强制性处理

## assert关键字
JDK1.4

外部类.内部类 内部类对象 = new 外部类().new 内部类();

内部抽象类可以定义在普通类，抽象类或接口内部

# Lamda表达式
JDK1.8开始提供支持
避免了复杂的面向对象结构的要求
SAM（Single Abstact Method）,只有一个抽象方法
只有函数式接口才可以北Lambda表达式所使用

Lambda格式：
方法没有参数：()->{}
方法有参数：(参数，参数)->{}
如果现在只有一行语句返回：(参数，参数)->语句

## 方法引用
引用静态方法：类名称::static 方法名称
引用某个实例对象的方法：实例化对象::普通方法
引用特定类型的方法： 特定类::普通方法
引用构造方法：类名称::new



@FunctionalInterface

**interface** IFunction<R> {

​	**public** R upper();

}



**public** **class** JavaDemo {

​	**public** **static** **void** main(String[] args) {

​		IFunction<String> fun = "www.bing.com" :: toUpperCase; 

​		System.***out\***.println(fun.upper());

​	}

}

WWW.BING.COM

比较大小：public int compareTo(String anotherString)

这是一个普通方法，如果要引用普通方法，则往往都需要实例化对象，但是如果说现在不想给出实例化对象，只是想引用这个方法，则就可以使用特定类来进行引用处理。

引用指定类中的方法

@FunctionalInterface //函数式接口

**interface** IFunction<P> {	

​	**public** **int** compare(P p1,P p2);

}



**public** **class** JavaDemo {

​	**public** **static** **void** main(String[] args) {

​		IFunction<String> fun = String ::compareTo;

​		System.***out\***.println(fun.compare("A", "a"));

​	}

}

在方法引用里面最具有杀伤力的就是构造方法的引用

引用构造方法：

**class** Person{

​	**private** String name;

​	**private** **int** age;

​	**public** Person (String name,**int** age ) {

​		**this**.name = name;

​		**this**.age = age;

​	}

​	@Override

​	**public** String toString() {

​		**return** "Person [name=" + name + ", age=" + age + "]";

​	}

}



@FunctionalInterface //函数式接口

**interface** IFunction<R> {

​	**public** R create(String s,**int** a);

}



**public** **class** JavaDemo {

​	**public** **static** **void** main(String[] args) {

​		IFunction<Person> fun = Person :: **new** ;

​		System.***out\***.println(fun.create("张三", 20));

​	}

}

提供方法引用的概念更多的情况下也只是弥补了对于引用的支持功能。



## 内建函数式接口

在JDK1.8之中提供有Lambda表达式也提供有方法引用，但是你会发现现在如果由开发者自己定义函数式接口“@FunctionalInterface”注解来进行大量声明，于是很多情况下如果为了方便，则可以直接引用系统中提供的函数式接口。

在系统之中专门提供有一个java.util.function的开发包，里面可以直接使用函数式接口。在这个包下面有如下的核心接口提供使用

1.功能性函数式接口：

| 接口定义：                                                   | 接口使用                                                     |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| @FunctionalInterface<br / >public interface Function<T,R>{<br /> public R apply(T t)<br />} | import java.util.function.Function;<br/><br/>public class JavaDemo {<br/>	public static void main(String[] args) {<br/>		Function<String, Boolean> function = "**hello" :: startsWith;<br/>		System.out.println(function.apply("**"));<br/>	}<br/>} |

2.消费型函数式接口：只能进行数据的处理操作，没有任何返回

- 在进行系统数据输出的时候使用的是System.out.println()

| 接口定义                                                     | 接口使用                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| @FunctionalInterface<br />public interface Consumer<T>{<br /></t>  public void accept(T t)<br />} | public class JavaDemo {<br/></t >public static void main(String[] args) {<br/></t ></t >Consumer<String> con = System.out :: println;<br/></t ></t >con.accept("www.bing.com");<br/>	}<br/>} |

3.供给型函数式接口：

在string类中提供有转小写方法，这个方法没有接受参数，但是有返回值；public	string toLowerCase();

| 接口定义                                                     | 接口使用                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| @FunctionalInterface<br />public interface Supplier<T>{<br /></t > public T get()<br />} | public class JavaDemo {<br/>	public static void main(String[] args) {<br/>		Supplier< String > sup = "www.bing.com" :: toLowerCase ;<br/>		System.out.println(sup.get());<br/> 	}<br/>} |

4.断言

| 接口定义                                                     | 接口使用                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| @FunctionalInterface<br />public interface Predicate<T>{<br /></t > public boolean test(T t)<br />} | public class JavaDemo {<br/>	public static void main(String[] args) {<br/>		Predicate<String> pre =  "bing" :: equalsIgnoreCase;<br/>		System.out.println(pre.test("BING"));<br/> 	}<br/>} |

以后对于实际项目开发之中,如果JDK本身提供的函数式接口可以被我们所使用,那么就没有不要重新定义



# 链表

进行链表操作的过程之中为了避免转型的异常应该使用泛型,同时也应该设计一个链表的执行标准的接口,同时具体实现该接口的时候还应该通过Node类做出节点的关系描述



# 线程

程序：是为了完成特定任务、用某种语言编写的一组指令的集合。即指一段静态的代码，静态对象。

进程：是程序的一次执行过程，或是正在运行的一个程序。是一个动态的过程：有它自身的产生、存在和小王的过程 --生命周期 说明：进程作为资源分配的单位，系统在运行时会为每个进程分配不同的内存区域

线程：进程可进一步细化为线程，是一个程序内部的一条执行路径。 说明：线程作为调度和执行单位，每个线程拥有独立的运行栈和程序计数器，线程切换的开销小。

并行：多个cpu同时执行多个任务。 并发：一个cpu（采取时间片）同时执行多个任务。

在Java程序执行的过程之中考虑到对于不同层次开发这的需求,所以其支持有本地的操作系统函数调用,而这项技术称为JNI技术,但是Java开发过程中并不推荐这样使用.

## 多线程的创建

方式一：继承于Thread类 

1. 创建一个继承于Thread类的子类
2. 重写Thread类的run() --> 将此线程执行的操作声明在run()中
3. 创建Thread类的子类的对象
4. 通过此对象调用start()

方式二：实现Runnable接口

1. 创建一个实现了Runnable接口的类
2. 实现类去实现Runnable中的抽象方法：run()
3. 创建实现类的对象
4. 将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
5. 通过Thread类的对象调用start()

比较创建线程的两种方式:

开发中：优先选择：实现Runnable接口的方式

原因：

1. 实现的方式没有类的单继承性的局限性

2. 实现的方式更适合来处理多个线程有共享数据的情况

   联系：public class Thread implements Runnable

   相同点：两种方式都需要重写run(),将线程要执行的逻辑声明在run()中。

多线程设计之中,使用了代理设计模式的结构,用户自定义的线程主题只是负责项目核心功能的实现,而所有的辅助实现全部交由Thread类来处理.

方法三:

使用Callable实现多线程处理

在进行Thread

一个Java应用程序java.exe，其实至少个线程：main()主线程，gc()垃圾回收线程，异常处理线程。如果发生一场会影响主线程

JDK中用Thread.State类定义了线程的几种状态 新建--->就绪--->运行--->阻塞--->死亡

/**

测试Thread中的常用方法
1.start():启动当前线程；调用当前线程run()
2.run():通常需要重写Thread类中的此方法，将创建的线程要执行的操作声明在此方法中
3.currentThread():静态方法，返回当前代码执行的线程
4.getName():获取当前线程的名字
5.setName():设置当前线程的名字
6.yield():释放当前cpu的执行权
7.join():在线程A中调用线程B的join()，此时线程A就进入阻塞状态，
知道线程B完全执行完后，线程A才结束阻塞状态。
8.stop():强制线程生命期结束，不推荐使用（已过时）
9.sleep(long millitime):让当前线程“睡眠”指定的millitime毫秒。
在指定的millitime毫秒时间内，当前线程是阻塞状态
10.isAlive():判断当前线程是否存活
*线程的优先级 *1.

MAX_PRIORITY: 10 最大
MIN_PRIORITY: 1 最小
NORM_PRIORITY: 5 默认 *2.如何获取和设置当前线程的优先级
getPriority():获取线程的优先级
setPriority(int p):设置线程的优先级
说明：高优先级的线程要抢占低优先级线程cpu的执行权。
但是只是从概率上讲，高优先级的线程高概率的情况先被执行。
并不意味着只有当高优先级的线程执行完以后，低优先级的线程才执行。
//设置分线程的优先级
线程名.setPriority(Thread.MAX_PRIORITY)





