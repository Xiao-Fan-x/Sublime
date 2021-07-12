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

1、参数列表必须完全与被重写方法的相同； 2、返回类型必须完全与被重写方法的返回类型相同； 3、访问级别的限制性一定不能比被重写方法的强； 4、访问级别的限制性可以比被重写方法的弱； 5、重写方法一定不能抛出新的检查异常或比被重写的方法声明的检查异常更广泛的检查异常 6、重写的方法能够抛出更少或更有限的异常（也就是说，被重写的方法声明了异常，但重写的方法可以什么也不声明） 7、不能重写被标示为final的方法； 8、如果不能继承一个方法，则不能重写这个方法。



继承的根本原因是因为要*复用*，而实现的根本原因是需要定义一个*标准*