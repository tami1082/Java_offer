## 重写
<p align="left">
  <Image src="pic/chongxie.png" width="947.5" height="247.5" />
</p>   

```java
// 为什么需要重写 alt+insert
// 父类的功能，子类 不一定需要，或不一定满足
// 静态方法和非静态有区别
// 没有static的时候子类重写了父类的方法，这个时候叫重写
// 重写关键词只有public
// 重载是参数列表不同，重写是子父类才有
// 重写需要有继承关系，子类对父类的方法
// 方法名字必须相同
// 参数列表相同
// 修饰符可以扩大，private > protected > default > private
// 抛出的异常，可以缩小，但不能扩大
// 重写都是方法的重写，和属性无关
```
## 多态
即同意方法可以根据发送对象的不同而采用多种不同的行为方法。  
一个对象的实际类型是确定的，但可以指向对象的引用的类型有很多（左边）。  
**多态是方法的多态，属性没有多态**  instanceof 类型转换  
<p align="left">
  <Image src="pic/duotai.png" width="822.5" height="300" />
  <Image src="pic/duotai2.png" width="882" height="291" />
</p>  

## instanceof 类型转换
```java
x instanceof y 看x和y有没有继承关系
父类引用指向子类的对象
把子类转换为父类，向上转换
把父类转换成子类，向下转型，强制转化
方便方法的调用，减少重复代码
```

## static
```java
/* 
第一次调用的时候，先执行 静态代码块 匿名代码块 构造方法
第二次调用的时候 匿名代码块 构造方法
 */
 /*
object > Person > student
object > Person > teacher
object > String
 */
 ```
 ## 抽象类
 只有方法名字没有方法，抽象类的所有方法都必须由子类重写，除非子类也是抽象不用写了  
 extends是单继承，接口是多继承。  
 不能new出来，只能考子类实现它。  
 抽象类可以写普通方法  
 抽象方法必须在抽象类里  
 
 ## 接口
 普通类：只有具体实现  
 抽象类：具体实现和规范都有  
 接口：只有规范，无法写方法，结束和实现分离  
 ```java
 package oop_A;

public interface oop_api {
    //常量
    public static final int AGE = 10;
    
    //接口中的所有定义其实都是抽象的 public
    public abstract void run ();
    void delete();
    void add();
}
```
```java
package oop_A;
// 类可以实现接口 implement 接口
// 实现接口的类，必需重写接口中的方法
public class UserService implements oop_api, Timeoop{
    @Override
    public void run() {

    }

    @Override
    public void delete() {

    }

    @Override
    public void add() {

    }

    @Override
    public void timer() {

    }
}
```
```java
package oop_A;

public interface Timeoop {


    void timer();
}
```

## 内部类
内部类就是在一个类的内部在定义一个类，比如A类中定义一个B类，那么B类相对A类来说就是内部类，反之是外部类。  
```java
package oop_A;

public class Outer {
    private int id = 10;
    public void run(){
        System.out.println("outer");
        class B {
            //局部内部类
        }
    }

    public class Inner{
        public void in(){
            System.out.println("in");
        }
        //获得外部类的私有属性
        public void getId(){
            System.out.println(id);
        }
    }
}
//一个java只能有一个public，但可以有多个class类
class A{

}

public static void main(String[] args) {
        //外部类直接new
        Outer outer = new Outer();
        //通过外部类实例化内部
        Outer.Inner inner = outer.new Inner();
        inner.getId();
    }
```
## 异常机制 exception
java把异常当作对象处理，java.lang.Throwable作为所有异常的超类。  
Error类对象由Java虚拟机生成并抛出，大多数错误与代码编写有关。  
Java虚拟机运行错误（virtual machinError）当jvm不在继续执行操作所需的内存资源时，将出现outofMemoryError。这些异常发生时，Java虚拟机一般会选择线程终止。  
还有发生在虚拟机试图执行应用时，如类定义错误（NoClassDefFoundError）等。  
在Exception分支中有一个重要的子类RuntimeException （运行时异常）；ArraylndexOutOfBoundsException （数组下标越界）；NullPointerException （2指针异常）；ArithmeticException （算术异常）；MissingResourceException （失资源）；ClassNotFoundException （找不到类）等异常。  
这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。  
◆这些异常一般是由程序逻辑错误引起的，程序应该从逻辑角度尽可能避免这类异常的发生；  
◆Error和Exception的区别： Error通常是灾难性的致命的错误，是程序无法控制和处理的，当出现这些异常时，Java虚拟机（JVM）一般会选择终止线程； Exception通常情况下是可以被程序处理的，并且在程序中应该尽可能的去处理这些异常。  

## 异常处理
 抛出异常；捕获异常。  
 异常处理关键字：try；catch; finally; throw; throws.  
 ```java
 import oop_A.Outer;
import oop_demo03.Person;
import oop_demo03.Student;

import java.io.ObjectStreamException;
import java.util.Scanner;

public class Application {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;
        // ctr alt t 自动生成
//        try {//try监控区域
//            System.out.println(a/b);
//        }catch (ArithmeticException e){ //catch想要捕获的异常类型 Throwable最高等级
//            System.out.println("为0");
//        }finally {
//            System.out.println("finally");
//        }
//        try {
//            if (b==0){ //主动抛出异常
//                throw new ArithmeticException();
//            }
//        } catch (Exception e) {
//            e.printStackTrace();
//        }

    }

    public void test(int a, int b) throws ArithmeticException{ //这个方法上抛出异常时 throws
        if (b==0){ //主动抛出异常
            throw new ArithmeticException(); // 一般在方法中使用
        }
    }
}
```

## 自定义异常
Java内部类可以处理大部分异常情况，用户自定义异常类，只需要继承exception类就行。  
◆在程序中使用自定义异常类，大体可分为以下几个步骤：  
1.创建自定义异常类。  
2.在方法中通过throw关键字抛出异常对象。  
3.如果在当前抛出异常的方法中处理异常，可以使用try-catch语句捕获并处理；否则在方法的声明处通过throws关键字指明要抛出给方法调用者的异常，继续进行下一步操作。  
4.在出现异常方法的调用者中捕获并处理异常.  

◆处理运行时异常时，采用逻辑去合理规避同时辅助try-catch处理  
◆在多重catch块后面，可以加一个catch （Exception）来处理可能会被遗漏的异常◆对于不确定的代码，也可以加上try-catch，处理潜在的异常  
◆尽量去处理异常，切忌只是简单地调用 printStackTrace（）去打印输出◆具体如何处理异常，要根据不同的业务需求和异常类型去决定  
◆尽量添加finally语句块去释放占用的资源  
```java
package oop_A;

public class MyException extends Exception{

    private int detail;

    public MyException(int detail) {

        this.detail = detail;
    }
    //toString alt+insert
    //异常打印信息

    @Override
    public String toString() {
        return "MyException{" +
                "detail=" + detail +
                '}';
    }
}

static void test(int a ) throws MyException {
        if (a>10){
            throw new MyException(a);
        }
    }

    public static void main(String[] args) {
        int a = 1;
        int b = 0;

        try {
            test(11);
        } catch (MyException e) {
            e.printStackTrace(); //打印一些信息
        }
    }
```





 
 
 
 
 
