# Java

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

| 方法                                          | 用途                                   |
| --------------------------------------------- | -------------------------------------- |
| Object clone()                                | 创建一个和被复制的对象完全一样的新对象 |
| boolean equals(Object object)                 | 判定对象是否相等                       |
| void finalize()                               | 在一个不常用的对象被使用前调用         |
| Class getClass()                              | 获取运行是一个对象的类                 |
| int hashCode()                                | 返回调用对象有关的散列值               |
| void notify()                                 | 恢复一个等待调用对象线程的执行         |
| void notifyAll()                              | 恢复所有等待调用对象线程的执行         |
|                                               |                                        |
| void wait()                                   | 返回描述对象的一个字符串               |
| void wait(long milliseconds)                  | 等待另一个线程的执行                   |
| void wait(long milliseconds, int nanoseconds) |                                        |





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



包装类相等判断的时候一定要使用equals判断



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

从最传统的开发来讲如果要进行多线程的实现肯定依靠的就是Runnable,但是Runnable接口有一个缺点：当线程执行完毕后无法获取一个返回值。从JDK1.5之后就提出了一个新的线程实现接口：java.util.concurrent.Callable接口

接口定义：

```java
@FunctionalInterface
public interface Callable<v>{
	public v call() throws Exception;        
}
```



```
class MyThread implements Callable<String>{
	@Override
	public String call() throws Exception{
		for()
		return "线程执行完毕";
	}
}
public class ThreadDemo{
	public static void main(String[] args){
		MyThread mythread = new MyThread();
		FutureTask<String> task = new FutureTask<>(mythread);
		new Thread(task).start();
		
	}
}
```

面试题：Runnable与Callable的区别？

Runnable是在JDK1.0的时候提出的多线程的实现接口，而Callable是在JDK1.5之后提出来的

Runnable接口之中只提供有一个run()方法，并且没有返回值。

Callable接口提供有call()方法，可以有返回值；

 * 1. call()可以有返回值的。
 * 2. call()可以抛出异常，被外面的操作捕获，获取异常的信息
 * 3. Callable是支持泛型的

方法四：

 * 创建线程的方式四：使用线程池
 *

 * 好处：

 * 1.提高响应速度（减少了创建新线程的时间）

 * 2.降低资源消耗（重复利用线程池中线程，不需要每次都创建）

 * 3.便于线程管理

 * corePoolSize：核心池的大小

 * maximumPoolSize：最大线程数

 * keepAliveTime：线程没有任务时最多保持多长时间后会终止

   
   
   ```
   //1. 提供指定线程数量的线程池
   ExecutorService service = Executors.newFixedThreadPool(3);
   ThreadPoolExecutor service1 = (ThreadPoolExecutor) service;
   //设置线程池的属性
   service1.setCorePoolSize(15);
   service1.setKeepAliveTime();
   //2.执行指定的线程的操作。需要提供实现Runnable接口或Callable接口实现类的对象
   service.execute(new NumberThread());//适合适用于Runnable
   service.execute(new NumberThread());//适合适用于Runnable
   //3.关闭连接池
   service.shutdown();
   ```

## 多线程

1.任何一个线程的对象，都应该使用Thread类进行封装，所以线程的启动使用的是start(),但是启动的时候将进入到一种就绪状态，现在并没有执行；

2.进入到就绪状态后就需要等待进行资源调度，当某一个线程调度成功之后则进入到运行状态（run()方法），但是所有的线程不可能一直持续执行下去，中间需要产生一些暂停的状态；

3.当run()方法执行完毕之后，实际上该线程的主要任务也就结束了，那么此时她可以直接进入到停止状态。



## 线程的命名与取得

构造方法：public Thread(Runnable target,String name);

设置名字：public final void setName(String name);

取得名字：public final String setName();

获取当前线程：public static Thread currentThread();



## 线程休眠

休眠：public static void sleep(long millis) throws InterruptedException;

休眠：public static void sleep(long millis,int nanos) throws InterruptedException;

在进行休眠的时候有可能会产生中断异常“InterruptedException”，中断异常属于Exception的子类，所以该异常必须进行处理。

休眠的主要特点是可以自动实现线程的唤醒，以继续进行后续的处理。



# 线程中断

线程的休眠里面提供有一个中断异常，实际上就证明线程的休眠是可以被打断的，而这种打断一定是由其他线程完成的。

判断线程是否被中断：public boolean isInterrupted()

中断线程执行：public void interrupt()



# 线程的强制执行

线程的强制执行指的是当满足于某些条件之后，某一个线程对象将可以一直独占资源，一直到该线程的程序执行结束。

强制执行：public final void join() throws InterruptedException

在进行线程强制执行的时候一定要获取强制执行线程对象之后才可以执行join



# 线程的礼让

线程的礼让值得是先将资源让出去让别的线程先执行。线程的礼让可以使用Thread中提供的方法

礼让：public static void yield()



# 线程的优先级

从理论上来讲线程的优先级越高越有可能先执行。

设置优先级：public final void setPriority(int newPriority)

获取优先级：public final int getPriority()

在进行优先级定义的时候都是通过int型数字来完成的，而对于此数字在选择在Thread类里面定义了三个常量

最高优先级：public static final int MAX_PRIORITY: 10 最大
最低优先级：public static final int MIN_PRIORITY: 1 最小
中等优先级：public static final int NORM_PRIORITY: 5 默认 

说明：高优先级的线程要抢占低优先级线程cpu的执行权。
但是只是从概率上讲，高优先级的线程高概率的情况先被执行。
并不意味着只有当高优先级的线程执行完以后，低优先级的线程才执行。



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



//设置分线程的优先级
线程名.setPriority(Thread.MAX_PRIORITY)

面试题：sleep() 和 wait()的异同？
1.相同点：

一旦执行方法，都可以使得当前的线程进入阻塞状态。
2.不同点：

1）两个方法声明的位置不同：Thread类中声明sleep() , Object类中声明wait()
2）调用的要求不同：sleep()可以在任何需要的场景下调用。 wait()必须使用在同步代码块或同步方法中
3）关于是否释放同步监视器：如果两个方法都使用在同步代码块或同步方法中，sleep()不会释放锁，wait()会释放锁。




# 同步问题

所谓的同步就是指

要在程序中实现这把锁的功能，就可以使用synchronized关键字来实现，利用此方法可以定义同步方法或者同步代码块，在同步代码块的操作里面的代码只允许一个线程执行。

1.利用同步代码块进行处理

```java
synchronized(同步对象){
	同步代码操作
}
synchronized (this) { //唯一对象
	同步代码操作
}
synchronized (类名.class) {	//多个对象
	同步代码操作
}
```

一般要进行同步对象处理的时候可以采用当前对象

加入同步处理之后，程序的整体的性能下降了。同步实际上会造成性能的降低。

2.利用同步方法解决：只需要在方法定义上使用synchronized关键字即可。

￼￼

```java
/**
 * 解决线程安全问题的方式三：Lock锁  --- JDK5.0新增
 *
 * 1. 面试题：synchronized 与 Lock的异同？
 *   相同：二者都可以解决线程安全问题
 *   不同：synchronized机制在执行完相应的同步代码以后，自动的释放同步监视器
 *        Lock需要手动的启动同步（lock()），同时结束同步也需要手动的实现（unlock()）
 *
 * 2.优先使用顺序：
 * Lock  同步代码块（已经进入了方法体，分配了相应资源）  同步方法（在方法体之外）
 */
```





# 程序死锁

死锁：若干个线程彼此互相等待的状态。

有的时候代码如果处理不当则会不定期出现死锁，这是属于正常开发中的调试问题

￼若干个线程访问同一资源时一定要进行同步处理，而过多的同步会造成死锁



# 利用Object类解决重复操作

死等：public final void wait() throws InterruptedException;

设置等待时间：public final void wait(long timeout) throws InterruptedException;

设置等待时间：public final void wait(long timeout,int nanos) throws InterruptedException;



唤醒第一个等待线程：public final void notify();

唤醒全部等待线程：public final void notifyAll();



# 停止线程

停止多线程：public void stop()

销毁多线程：public void destory()

挂起线程：public final void suspend()、暂停执行

恢复挂起的线程执行：public final void resume()

但在JDK1.2之后废除（不推荐用）

主要原因是因为这些方法有可能导致线程的死锁



## 后台守护线程

如果现在主线程的程序或者其他的线程还在执行的时候，那么守护线程一直存在，并且运行在后台状态。

在Thread类里面提供有如下的守护线程的操作方式：

设置守护线程：public final void setDaemon(boolean on);

判断是否为守护线程：public final boolean isDaemon();



实例：使用守护线程

守护线程是随着整体线程而存在的，如果程序执行完毕守护线程就消失了，最大的守护线程就是GC线程。程序执行中GC线程会一直存在，如果程序执行完毕，GC线程也将消失。



## transient关键字

声明的实例对象，只能在内存中储存，当对象存储时，它的值不需要维持

（无法被序列化）

## volatile关键字

**在多线程的定义之中，volatile关键字主要是在属性定义上使用的，表示此属性为直接数据操作，而不进行副本的拷贝处理。**这样的话在一些书上就将其错误的理解为同步属性了。

在正常进行变量处理的时候会经历如下步骤：

1.获取变量原有的数据内容副本

2.利用副本为变量进行数学计算

3.将计算后的变量，保存到原始空间之中

而如果一个属性上追加了volatile关键字，表示的就是不使用副本，而是直接操作原始变量，相当于节约了：拷贝副本，重新保存的步骤

面试题：请解释volatile与synchronized的区别？

volatile主要在属性上使用，而synchronized是在代码快与方法上使用的。

volatile无法描述同步的处理，它只是一种直接内存的处理，避免了副本的操作，而synchronized是同步操作



## 序列化

## Serializable接口

## Exteranlizable接口

实现`Externalizable`接口的类必须要提供⼀个`public`的⽆参的构造器。

static全局变量不会被序列化

可序列化类的所有⼦类型本⾝都是可序列化的

## strictfp关键字

一旦使用了strictfp来声明一个 类、接口或者方法时，那么所声明的范围内Java的编译器以及运行环境会完全依照浮点规范IEEE-754来执行。因此如果你想让你的浮点运算更加精确， 而且不会因为不同的硬件平台所执行的结果不一致的话，那就请用关键字strictfp。 

你可以将一个类、接口以及方法声明为strictfp，但是不允许对接口中的方法以及构造函数声明strictfp关键字



### StringBuffer类

每一个字符串的常量都属于一个String类的匿名对象，并且不可更改

身体日那个有两个常量池：静态常量池、运行时常量池

String类对象实例化建议使用直接复制的形式完成，这样可以直接将对象保存在对象池之中以方便下次重用

其最大弊端：内容不允许修改。

StringBuffer类可以实现字符串的修改



| 1    | public StringBuffer append(String s) 将指定的字符串追加到此字符序列。 |
| ---- | ------------------------------------------------------------ |
| 2    | public StringBuffer reverse()  将此字符序列用其反转形式取代。 |
| 3    | public delete(int start, int end) 移除此序列的子字符串中的字符。 |
| 4    | public insert(int offset, int i) 将 `int` 参数的字符串表示形式插入此序列中。 |
| 5    | insert(int offset, String str) 将 `str` 参数的字符串插入此序列中。 |
| 6    | replace(int start, int end, String str) 使用给定 `String` 中的字符替换此序列的子字符串中的字符。 |

StringBuffer类从JDK1.0开始提供

StringBuilder类从JDK1.5开始提供，与StringBuffer功能相同

StringBuffer类方法线程安全

StringBuilder类方法非线程安全（快）



### CharSequence借口

只要有字符串就可以为CharSequence借口实例化

CharSequence本身是一个借口，

| `char`              | `charAt(int index)`Returns the `char` value at the specified index. |
| ------------------- | ------------------------------------------------------------ |
| `default IntStream` | `chars()`Returns a stream of `int` zero-extending the `char` values from this sequence. |
| `default IntStream` | `codePoints()`Returns a stream of code point values from this sequence. |
| `int`               | `length()`Returns the length of this character sequence.     |
| `CharSequence`      | `subSequence(int start,           int end)`Returns a `CharSequence` that is a subsequence of this sequence. |
| `String`            | `toString()`Returns a string containing the characters in this sequence in the same order as this sequence. |



### AutoCloseable

主要用于资源开发的处理上，以实现资源的自动关闭（释放）

例如：文件、网络、数据库开发的过程中由于服务器的资源有限，所以使用后一定要关闭。

JDK1.7

关闭方法：

| Modifier and Type | Method and Description                                       |
| :---------------- | :----------------------------------------------------------- |
| `void`            | `void close()  throws Exception`关闭此资源，放弃任何基础资源。 |

要想实现自动关闭处理，除了要使用AutoCloseable之外，还要结合一场处理语句才可以正常使用



## Runtime类（JDK1.0）

描述的是运行时的状态，也就是说在整个JVM之中，Runtime类是唯一一个与JVM运行状态有关的类，默认提供有一个该类的实例化对象。

在每一个JVM进程里面只允许提供有一个Runtime类的对象，所以这个类的构造方法默认私有化了，该类使用的是单例设计模式，并且单例设计模式一定会提供有一个static方法获取本类实例。

由于Runtime类属于单例设计模式，如果想要获取实例化对象，可以依靠类中的getRuntime()方法完成，

获取实例化对象：public static Runtime getRuntime()

获取空闲内存空间：public long freeMemory()

获取可用内存空间：public long totalMemory()本电脑内存的1/64

获取最大内存空间：public long maxMemory()本电脑内存的1/4

手动进行GC处理：public void gc()

long以字节为单位返回

面试题：什么是GC？如何处理？

GC是garbage collector垃圾收集器，是可以由系统自动调用的垃圾释放功能，或者使用Runtime类中的gc()手工调用



### system类

数组拷贝：public static void arraycopy(Object src,
                             int srcPos,
                             Object dest,
                             int destPos,
                             int length)

获取当前的日期时间数值：public static long currentTimeMillis()

操作耗时的统计：单位毫秒



进行垃圾回收：public static void gc()

gc()操作为（Runtime.getRuntime().gc()）并不是重新定义



### cleaner类

JDK1.9提供的一个对象清理操作，其主要的功能是进行finalize()方法的代替

C++中的析构函数（对象手工回收），在Java中所有的垃圾空间都是通过GC自动回收，很多情况下不使用这类析构函数，因此Java并没有提供这方面的支持

但Java本身依然提供了给用户收尾的操作，

@Deprecated(since="9")
protected void finalize() throws Throwable 不建议使用

最大的特点是抛出一个Throwable异常类型，这个异常了类型分为两个子类型：Error和Exception,平常处理的都是Exception

从JDK1.9开始建议开发之使用AutoCloseable或者使用java.lang.ref.Cleaner类进行回收处理

（Cleaner也支持有AutoCloseable处理）



### clone类

protected Object clone() throws CloneNotSupportedException

所有的类都会继承Object父类，所以所有的类都一定会有clone()方法，但并不是所有的类都希望被克隆，所以如果想要对象克隆，那么对象所在的类需要实现一个Cloneable接口，此借口并没有任何的方法，是因为它描述的是一种能力。

例子：实现对象的克隆

```java
public class Test {
    public static void main(String[] args) throws CloneNotSupportedException {
        Member memberA = new Member("xiaofan",16);
        Member memberB = (Member) memberA.clone();
        System.out.println(memberA.toString());
        System.out.println(memberB.toString());
    }
}

class Member implements Cloneable{
    private String name;
    private int age;

    public Member(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return super.toString()+
                " Member{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

Member@677327b6 Member{name='xiaofan', age=16}
Member@14ae5a5 Member{name='xiaofan', age=16}



# 数字操作

### Math数学

Math类里面提供的基本上都是基础的数学公式，需要的时候需要自己重新整合

### Random类

产生一个不大于边界的随即非负整数：public int nextInt(int bound)

### 大数字操作类

两个大数字的操作类：BigInteger、BigDecimal

求余：public BigInteger[] divideAndRemainder(BigInteger val)数组第一个为商第二个为余数

BigDecimal与BigInteger操作是非常类似的，都有基础的数学支持

BigDecimal有进位的问题

除法计算：@Deprecated(since="9")
public BigDecimal divide(BigDecimal divisor,
                         int scale,
                         int roundingMode)

## Date类

时间用的都是毫秒

将long转为Date：public Date(long date)

将Date转为long：public long getTime()

## 格式化日期

SimpleDateFormat

DateFormat继承 将日期格式化：public final String format(Date date)

DateFormat继承 将字符串转为日期：public Date parse(String source) throws ParseException

构造方法：public SimpleDateFormat(String pattern)

 	日期格式：年（yyyy）、月（MM）、时（HH）、分（mm）、秒（ss）、毫秒（SSS）、

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Test {
    public static void main(String[] args) throws CloneNotSupportedException, ParseException {
        Date date = new Date();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String str = sdf.format(date);
        System.out.println(str);
    }
}
```

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Test {
    public static void main(String[] args) throws CloneNotSupportedException, ParseException {
        String birthday = "1999-10-20 10:10:10";
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date date = sdf.parse(birthday);
        System.out.println(date);
    }
}
```



如果在进行字符串定义的时候，所使用的日期时间数字超过了制定的合理范围，则会自动进行进位



# 正则表达式

1.单个字符匹配

任意字符 表示由任意字符组成

\\：匹配“\”

\n :匹配换行

\t ：匹配制表符

2.字符集

[abc]:表示可能是字母a、b、c中的任意一个

[^abc]:非abc中的任意一个

[a-zA-Z\] : ]:示由一个任意字母所组成，不区分大小写

\s :空白的制表符

\S匹配任意的非空格数据

\w：匹配字母、数字、下划线，等价于“[a-zA-Z_0-9]”

\W  :匹配非字母、数字、下划线，等价于“[a-zA-Z_0-9]”

3.边界匹配：

^匹配边界开始

¥匹配边界结束

4.数量表示，默认情况下只有添加上了数量单位才可以匹配多位字符

？：0次或1次

*：0次、1次或多次

+：1次或多次

{n}: 表达式的长度正好为n次

{n,}表达式的长度为n次以上

表达式{n,m}:表达式的长度在n～m

5.逻辑表达式

XY		X｜Y 		



## String类对正则的支持



## java.util.regex开发包

1.Partern类提供有正则表达式的编译处理支持：

public static Pattern compile(String regex)

同时也提供有字符串的拆分操作：

public String[] split(CharSequence input)

```java
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        String str = "daddsdad()dasddasf$$()dsadffds()$dasd$%ds";
        String regex = "[^a-zA-Z]";
        Pattern pat = Pattern.compile(regex);
        System.out.println(pat);
        String res[] = pat.split(str);
        for (int i =0;i<res.length;i++){
            System.out.println(res[i]);
        }
    }
}
```

2.Matcher类，实现了正则匹配的处理类，这个类的对象实例化依靠Pattern类完成

Pattern类提供的方法：public Matcher matcher(CharSequence input)

当获取了Matcher类的对象之后就可以利用该类中的方法进行如下操作

正则匹配：public boolean matches()

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        String str = "101";
        String regex = "\\d+";
        Pattern pat = Pattern.compile(regex);
        Matcher mat = pat.matcher(str);
        System.out.println(mat.matches());
    }
}
```

如果纯粹以拆分、替换、匹配三种操作根本用不到java.util.regex开发包，只依靠String类就都可以实现了。但是Matcher类中提供有一种分组的功能，而这种分组的功能是String不具备的

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        String str = "iaodjsadjosa#{dasd}()dsdad";
        String regex = "#\\{\\w+\\}";
        Pattern pat = Pattern.compile(regex);
        Matcher mat = pat.matcher(str);
        while (mat.find()){
            System.out.println(mat.group(0).replaceAll("#|\\{|\\}",""));
        }
    }
}
```



# 国际化程序实现

同一个国家可以根据不同国家实现不同的语言描述，但是程序核心业务是相同的

利用区域编码加载显示文字信息

1.如何可以定义保存文字的文件信息

2.如何可以根据不同的区域语言的编码读取指定的资源信息



## locale类

一个专门描述区域和语言编码的类：Locale

构造方法：public Locale（String language);

构造方法：public Locale（String language,String country);

需要的是国家和语言的代码，而中文的代码：zh_CN、美国英国的代码：en_US

对于这些区域和语言的编码，最简单的获得方式就是可以通过IE浏览器

```java
import java.util.Locale;

public class Test {
    public static void main(String[] args) {
        Locale loc = new Locale("zh","CN");
        System.out.println(loc);
    }
}
```

手工选择文字

自动获得当前的运行环境：

读取本地默认环境：public static Locale getDefault()

在实际的开发过程之中，为了简化开发，Locale也将世界上一些比较著名的国家编码设置为常量；

使用常量的优势在于可以避免一些区域编码信息的繁琐。



## 读取资源文件：ResourceBundle

已经准备好了资源文件：那么随后就需要进行资源文件的读取操作了，二读取资源文件主要依靠的java.util.ResourceBundle类

public abstract class ResourceBundle extends Object

ResourceBundle是一个抽象类，如果说现在要想进行此类对象的实例化可以直接使用一个静态方法

public static final ResourceBundle getBundle(String baseName)

basename描述的是资源文件的名称（.properties文件），但是没有后缀

读取资源内容：public final String getString(String key);

如果资源没有放在包里面，则直接编写资源名称即可

在进行资源读取的时候数据的key一定要存在，如果不存在则会出现如下异常：

java.util.MissingResourceException:

错误的资源异常

使用ResourceBundle读取内容

public static final ResourceBundle getBundle(String baseName,
                                             Locale locale)

读取顺序：读取指定区域的资源文件>默认的本地资源>公共的资源

```java
import java.util.ResourceBundle;

public class Test {
    public static void main(String[] args) throws Exception{
        ResourceBundle resource = ResourceBundle.getBundle("ali.message.Message");
        String val = resource.getString("info");
        System.out.println(val);
    }
}
```

```java
import java.util.Locale;
import java.util.ResourceBundle;

public class Test {
    public static void main(String[] args) throws Exception{
        Locale loc = new Locale("en","US");
        ResourceBundle resource = ResourceBundle.getBundle("ali.message.Message",loc);
        String val = resource.getString("info");
        System.out.println(val);
    }
}
```

```properties
# Message_en_US.properties
info=Welcome!
```

```properties
# Message_zh_CN.properties
info=你好！
```

如果有指定区域的资源文件存在的时候，那么没有设置区域的资源文件的信息将不会被读取



## 格式化文本显示

修改资源文件

中文资源文件

info=你好，{0}！今天是{1}。

英文资源文件

Welcome {0},date {1}.

需要MessageFormat类进行格式化处理，Format类的子类

public static String format(String pattern,
                            Object... arguments)

```java
import java.text.MessageFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;
import java.util.ResourceBundle;

public class Test {
    public static void main(String[] args) throws Exception{
        Locale loc = new Locale("en","US");
        ResourceBundle resource = ResourceBundle.getBundle("ali.message.Message",loc);
        String val = resource.getString("info");
        System.out.println(MessageFormat.format(val,"csdn",new SimpleDateFormat("yyyy-MM-dd").format(new Date())));
    }
}
```

```properties
info=你好！{0},日期{1}。
```



## UUID

UUID是一种生成无重复字符串的一种程序类，这种程序类的主要功能是根据时间戳实现一个自动的无重复的字符串定义。重复的概率千万分之一（intel曾经出现过重复并且造成巨大损失）

获取UUID：public static UUID randomUUID()

根据字符串获取UUID内容：public static UUID fromString(String name)

在对一些文件进行自动命名处理的情况下，UUID类型非常好用。



## Optional类

主要功能是进行null的相关处理，在进行程序开发的时候，如果为了防止程序之中出现空指向异常，



## ThreadLocal类

构造方法：public ThreadLocal();

设置数据：public void set( T value );

取出数据：public T get();

删除数据：public void remove();

每一个线程通过ThreadLocal只允许保存一个数据

```java
public class JavaAPIDemo {
    public static void main(String[] args) {
        new Thread(()->{
            Message msg1 = new Message();
            msg1.setInfo("第一个线程");
            Channel.setMessage(msg1);
            Channel.send();
        },"线程一").start();
        new Thread(()->{
            Message msg2 = new Message();
            msg2.setInfo("第二个线程");
            Channel.setMessage(msg2);
            Channel.send();
        },"线程二").start();
        new Thread(()->{
            Message msg3 = new Message();
            msg3.setInfo("第三个线程");
            Channel.setMessage(msg3);
            Channel.send();
        },"线程三").start();
    }
}

class Channel{
    private static final ThreadLocal<Message> THREADLOCAL = new ThreadLocal<Message>();
    private Channel(){}
    public static void setMessage(Message m){
        THREADLOCAL.set(m);
    }
    public static void send(){
        System.out.println(Thread.currentThread().getName()+"[消息发送]"+ THREADLOCAL.get().getInfo());
    }
}

class Message{
    private String info;
    public void setInfo(String info){
        this.info = info;
    }
    public String getInfo() {
        return info;
    }
}
```



## 定时器

定时器主要操作时进行定时任务的处理

Java中提供有定时任务的支持，但只支持间隔出发的操作。

一个接口一个类

java.util.TimerTask类：实现定时任务处理

java.util.Timer类：进行任务的启动，启动的方法

​	任务启动：public void schedule(TimerTask task,long delay);延迟单位为毫秒

public void scheduleAtFixedRate(TimerTask task,
                                long delay,
                                long period)

```java
import java.util.Timer;
import java.util.TimerTask;

public class JavaAPIDemo {
    public static void main(String[] args) {
        Timer timer = new Timer();
        timer.schedule(new MyTask(),100,1000);
    }
}
class MyTask extends TimerTask{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"、定时任务执行，当前时间"+System.currentTimeMillis());
    }
}
```





## base64加密与解密



Base64.Encoder：加密处理

​	public byte[] encode(byte[] src)

Base64.Decoder:解密处理

​	public byte[] decode(String src)

```java
import java.util.Base64;

public class JavaAPIDemo {
    public static void main(String[] args) {
        String msg = "www.baidu.com";
        String encmsg = new  String(Base64.getEncoder().encode(msg.getBytes()));
        System.out.println(encmsg);
        String oldMsg = new String(Base64.getDecoder().decode(encmsg));
        System.out.println(oldMsg);
    }
}
```



盐值加密算法

```
public class JavaAPIDemo {
    public static void main(String[] args) {
        String msg = "www.baidu.com";
        String encmsg = new  String(Base64.getEncoder().encode(msg.getBytes()));
        System.out.println(encmsg);
        String oldMsg = new String(Base64.getDecoder().decode(encmsg));
        System.out.println(oldMsg);
    }
}
```

多次加密

```java
import java.util.Base64;

class StringUtil{
    private static final String SALT = "wwwcom";
    private static final int REPEAT = 3;
    /**
     * SALT:需要加密的字符串，需要与盐值整合
     * REPEAT：加密的重复次数
     * return：加密后的数据
     */

    public static String encode(String str){
        String temp = str + "{" + SALT + "}";
        byte[] data = temp.getBytes();
        for (int i = 0; i < REPEAT; i++) {
            data = Base64.getEncoder().encode(data);
        }
        return new String(data);
    }

    public static String decode(String str){
        byte[] data = str.getBytes();
        for (int i = 0; i < REPEAT; i++) {
            data = Base64.getDecoder().decode(data);
        }
        return new String(data).replaceAll("\\{[a-zA-Z]]\\}","");
    }
}

public class JavaAPIDemo {
    public static void main(String[] args) {
        String msg = "www.baidu.com";
        String str = StringUtil.encode("www.baidu.com");
        System.out.println(str);
        System.out.println(StringUtil.decode(str));
    }
}
```

复杂加密

最好的做法是使用2-3中加密程序，同时再找到一些完全不可解密的加密算法。



# 比较器



comparable接口

comparator比较器

在Arrays类里面排序有另外一种实现：

：public static <T> void sort(T[] a, Comparator<? super T> c);

不建议使用comparator

面试题：请解释Comparator与Comparable的区别？

​	java.lang.Comparable是在类定义的时候实现的父接口，主要用于定义排序规则，里面主要有comparaTo()方法

​	java.util.Comparator是挽救的比较器操作，需要设置单独的比较器规则类实现排序，里面主要是compare()方法



## 二叉树结构

时间复杂度O(logn)

二叉树：前序，中序，后序

```java
import java.time.chrono.IsoChronology;

public class BinaryTree<T extends Comparable<T>> {

    private class Node {
        private Comparable<T> data;//存放comparable，可以比较大小
        private Node parent;    //保存父节点
        private Node left;
        private Node right;

        public Node(Comparable<T> data) {
            this.data = data;
        }

        public void addNode(Node newNode) {
            if (newNode.data.compareTo((T) this.data) <= 0) {
                if (this.left == null) {
                    this.left = newNode;
                    newNode.parent = this;
                } else {
                    this.left.addNode(newNode);
                }
            } else {
                if (this.right == null) {
                    this.right = newNode;
                    newNode.parent = this;
                } else {
                    this.right.addNode(newNode);
                }
            }
        }

        //获取所有数据，中序遍历
        public void toArrayNode() {
            if (this.left != null) {
                this.left.toArrayNode();
            }
            BinaryTree.this.returnData[BinaryTree.this.foot++] = this.data;
            if (this.right != null) {
                this.right.toArrayNode();
            }
        }
    }

    private Node root;
    private int count;
    private Object[] returnData;
    private int foot = 0;//脚标控制


    public void add(Comparable<T> data) {
        if (data == null) {
            throw new NullPointerException("保存的数据不能为空");
        }
        Node newNode = new Node(data);
        if (this.root == null) {
            this.root = newNode;
        } else {
            this.root.addNode(newNode);
        }
        this.count++;
    }

    public Object[] toArray() {
        if (this.count == 0) {
            return null;
        }
        this.returnData = new Object[this.count];//保存长度为数组长度
        this.foot = 0;//脚标清零
        this.root.toArrayNode();
        return this.returnData;
    }

}
```

## 数据删除





```java
if(args.length != 1){

​	System.out.println(" ");

​	System.exit(1);

}	
```



```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        String str = "<font face=\"Arial,Serif\"size=\"+2\" color=\"red\">";
        String regex = "\\w+=\"[a-zA-Z0-9,\\+]+\"";
        Matcher matcher = Pattern.compile(regex).matcher(str);
        while (matcher.find()){
            String temp = matcher.group(0);
            String result[] = temp.split("=");
            System.out.println(result[0]+"\t"+result[1].replaceAll("\"",""));
        }
    }
}
```

## 红黑树

本质就是在节点上追加了一个表示颜色的操作信息

```java
enum Color{	//枚举类
	RED,BLACK;
}

class BinaryTree<T>{
	private T data;
	private Node parent;
	private Node left;
	private Node right;
	private Color colo;
}
```

Node节点中的颜色标记也可以使用true和false表示，不一定要使用枚举类

![image-20210706194111037](C:\Users\Xiao\AppData\Roaming\Typora\typora-user-images\image-20210706194111037.png)





# Java的I/O编程

java.io.File

File类是唯一一个与文件本身操作（创建、删除、重命名等等）有关的，需要文件完整路径

构造方法：public File(String pathname)

构造方法：public File(String parent,String child) 设置父路劲与子目录

创建新的文件：public boolean createNewFile() throws IOException

判断文件是否存在：public boolean exists()

删除文件：public boolean delete()



windows下的分隔符“\”，Linux下的分隔符“/”,File类提供有一个常量：

public static final String separator



获取父路径：public File getParentFile()

创建目录：public boolean mkdirs()

文件可读：public boolean canRead()

文件可写：public boolean canWrite()

文件的大小（字节）：public long length()

最后的修改时间：public long lastModified()

是否为目录：public boolean isDirectory()

是否为文件：public boolean isFile()

目录文件public File[] listFiles()

```java
import java.io.File;

public class Test {
    public static void main(String[] args) {
        File file = new File("C:\\Users\\Xiao\\Pictures\\雷蛇壁纸");
        long start = System.currentTimeMillis();
        renameDir(file);
        long end = System.currentTimeMillis();
        System.out.println(end - start);
    }
    private static void renameDir(File file) {
        if (file.isDirectory()) {
            File results[] = file.listFiles();
            if (results != null) {
                for (int x = 0; x < results.length; x++) {
                    renameDir(results[x]);
                }
            }
        } else {
            if (file.isFile()) {
                String filename = null;
                if (file.getName().contains(".")){
                    filename = file.getName().substring(0,file.getName().lastIndexOf("."))+".png";
                }else {
                    filename = file.getName()+".png";
                }
                File newFile = new File(file.getParentFile(),filename);
                file.renameTo(newFile);
            }
        }
    }
}
```



## java字节流操作

字节处理流：OutputStream（输出字节流）、InputStream（输入字节流）

字符处理流：Writer（输出字符流）、Reader（输入字符流）



所有的流操作都应该采用统一的步骤进行：文件处理的流程



文件的读写操作，通过File类找到一个文件路径

通过字节流或字符流的子类为弗雷对象实例化

利用字节流或字符流中的方法是西安数据的输入与输出操作

流的造作属于资源操作，资源操作必须进行关闭处理



## OutputStream 类

字节的数据已byte类型为主的操作

public abstract class OutputStream extends Object implements Closeable, Flushable



| 方法                                                         | 类型 |                  |
| ------------------------------------------------------------ | ---- | ---------------- |
| public abstract void write(int b)<br/>                    throws IOException | 普通 | 输出单个字节数据 |
| public void write(byte[] b)<br/>           throws IOException | 普通 | 输出一组字节数据 |
| public void write(byte[] b,<br/>                  int off,<br/>                  int len)<br/>           throws IOException | 普通 | 输出部分字节数据 |



覆盖：public FileOutputStream(File file)
                 throws FileNotFoundException

追加：public FileOutputStream(File file,
                        boolean append)
                 throws FileNotFoundException

使用OutputSteam类实现内容输出：



## Native关键字 Java Native Interface(JNI)

为声明一个本机方法，在该方法之前用native修饰符，但是不要定义任何方法体。例如：

public native int meth() ;

## 字符串处理

实现固定的，不可变的字符串比实现可变的字符串更高效

regionMatches( )方法将一个字符串中指定的区间和另一字符串中指定的区间进行比

较。它的重载形式允许在比较时忽略大小写。

startsWith( )方法判断一个给定的字符串（String）是否从一个指定的字符串开始。

endsWith( )方法判断所讨论的字符串（String）是否是以一个指定的字符串结尾。

使用concat( )可以连接两个字符串

trim( )方法返回一个调用字符串的拷贝，该字符串是将位于调用字符串前面和后面的空

白符删除后的剩余部分

//StringBuffer

而通过调用capacity( )方法可

以得到总的分配容量

ensureCapacity( ) 设置缓冲区的大小。这在事先已知要在StringBuffer上追加大量小字符串的情况下是有用的

void setLength(int len) 

这里len指定了缓冲区的长度。这个值必须是非负的。

reverse( ) 

## RunTime

void addShutdownHook(Thread thrd) 

当Java虚拟机终止时，寄存器thrd作为线程而运行





# 单例设计模式 双重校验锁

```java
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
        if (singleton == null) {  
            singleton = new Singleton();  
        }  
        }  
    }  
    return singleton;  
    }  
    
    private Object readResolve() {
        return singleton;
    }
}  
```

主要在Singleton中定义readResolve方法，并在该方法中指定要返回的对象的生成策略，就可以防止单例被破坏。

