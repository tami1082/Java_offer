## java方法/函数
java 方法是语句的集合，他们在一起执行一个功能  
命名方法，首字母小写，后面驼峰  
**方法包含于类或对象中；方法在程序中被创建，在其他地方引用；一个方法只完成一个功能**  
```java
修饰符 返回值 方法名（参数类型 参数名）{
//方法
return 返回值；}
```
◆修饰符：修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。  
◆返回值类型：方法可能会返回值。returnValueType是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下， returnValueType是关键字void。  
◆方法名：是方法的实际名称。方法名和参数表共同构成方法签名。  
◆参数类型：参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。  
  ◆形式参数：在方法被调用时用于**接收外界输入的数据**。  
  ◆实参：调用方法时**实际传给方法的数据**。  
◆方法体：方法体包含具体的语句，定义该方法的功能。  
调用方法：对象名.方法名（实参列表）  
当方法返回一个值的时候，方法调用通常被当作一个值
```java
int lar = max(30,40);
```
当方法返回值是void，方法调用一定是一条语句
```java
System.out.println("hh");
```
**值传递（Java）和引用传递**  
值传递：在方法被调用时，实参通过形参把它的内容副本传入方法内部，此时形参接收到的内容是实参值的一个拷贝，因此在方法内对形参的任何操作，都仅仅是对这个副本的操作，不影响原始值的内容。  
引用传递：”引用”也就是指向真实内容的地址值。在方法调用时，实参的地址通过方法调用被传递给相应的形参，在方法体内，形参和实参指向同一个内存地址，对形参的操作会影响真实内容。  
所以：在Java中不存在纯粹的引用传递。（C语言中基于指针的引用传递，才是纯粹的引用传递；Java形参赋值新的对象，对引用方是不可见的，当然，这种约束也避免了一些复杂的地址指向问题）  
## 方法重载
重载就是在一个类中，有相同的函数名称，但形参不同的函数。  
规则：方法名称必须相同；参数列表必须不同（个数，类别，参数排列顺序不同等）；方法的返回类型可以相同也可以不相同；仅仅返回类型不同不足以成为方法的重载。  
## 命令行传参
```java
package method;

public class Demo02 {
    public static void main(String[] args) {
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```
## 可变参数
在方法声明中，指定参数类型后加一个省略号（。。。）。一个方法中只能指定一个可变参数，他必须是最后一个参数  
```java
public class Demo02 {
    public static void main(String[] args) {
//        for (int i = 0; i < args.length; i++) {
//            System.out.println(args[i]);
//        }
        //如果没有函数声明了static的话想要引用要先声明！
        Demo02 d2 = new Demo02();
        d2.test(1,2,3,4,5,6,7,8); //啥也不传输出了一个 不知道是啥的东西 [I@58ceff1
    }

    //有时候一个重载写好几次，可变参数
    public void test(int x, int ... i ){
        for (int j = 0; j < i.length; j++) {
            System.out.println(i[j]);
        }
    }
}
```
## 递归
递归终止条件：什么时候不调用自身，如果没有就死循环了  
递归体：什么时候需要调用  
```java
public class DiGui {
    public static void main(String[] args) {
        DiGui dg = new DiGui();
        int n = 4;
        int res = dg.test(n);
        System.out.println(res);
    }
    public int test(int n){
        if(n==1){return 1; //递归终止条件
        }else{
            return n*test(n-1);
        }
    }
}
```
```java
package method;

import java.util.Scanner;

public class CalAdd {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        double num1 = 0;
        double num2 = 0;
        String c = null;
        while (scanner.hasNextDouble()) {
            num1 = scanner.nextDouble();
            c = scanner.next();
            num2 = scanner.nextDouble();
        }
        CalAdd ca = new CalAdd();
        double res = ca.cal(num1, c, num2);
        System.out.println(res);
        scanner.close();
    }
    public double cal(double num1, String str, double num2){
        double res = 0;
        if(str.length()==0){
            return 0;
        }else{
            switch (str){
                case "+":
                    res = num1+num2;
                    break;
                case "-":
                    res = num1-num2;
                    break;
                case "*":
                    res = num1*num2;
                    break;
                case "/":
                    res = num1/num2;
                    break;
                default:
                    break;
            }

        }
        return res;
    }
}
```
注意一下next()各种函数的用法有些区别
