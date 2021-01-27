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