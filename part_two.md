## package
为了更好地组织类，Java提供了包机制，用于区别类名的命名空间  
本质是文件夹，一般是公司域名为包名，包里面的名字尽量不要重复    
```java
(import) package pkg1[. pkg2[. pkg3...]];
```
<p align="middle">
  <img src="pic/package.png" width="283" height="372" />  
</p> 

## Java doc
javadoc 命名使用开生成自己API文档  
参数：  
@author 作者名		@version 版本号		@since 指明需要最早使用的jdk版本		@param 参数名		@return 返回值情况		@throws 异常抛出情况  
[jdk11 帮助文档](https://docs.oracle.com/en/java/javase/11/)  
<p align="left">
  <img src="pic/build_doc.png" width="670" height="371" />  
	<img src="pic/idea-doc.png" width="326" height="372" />  
</p> 

## java控制流
next(): 一定要读取到有效字符才可以阶数输入；对输入有效字符之前遇见的空白，next会自动去掉；只有输入有效字符后才将其后面输入的空白作为分隔符或结束符；**next不能得到带有空格的字符串**  
nextline(): 以enter为结束，以回车键之前所有输入为输出
```java
package base;

import java.util.Scanner;

public class Flow {
    public static void main(String[] args) {
//        scanner 对象 程序和人的交互 java.util.Scanner
//        Scanner s = new Scanner(System.in);
//        通过Scanner类的next()与nextLine()方法获取输入的字符串
//        在读取前我们一般需要使用hasNext(), hasNextLine()判断是否还有输入的数据
        Scanner s = new Scanner(System.in);
        System.out.println("output ");
        if (s.hasNext()){
//	if (s.hasNextLine()){ //这个if没关系，可以不用就是试试
            String str = s.next(); // 用next的输出 “hallo a” 只有“hallo"
	    String str1 = s.nextLine(); // 输出正常的 hallo a
            System.out.println("out " + str);
        }
        s.close(); //用完关掉，IO流不关就会一直占用资源

    }
}
```
```java
import java.util.Scanner;
//输入多个数字，求其总和和平均数，每输入一个数字回车确认，非数字结束，并输出
public class Flow_test {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        double sum = 0;
        int m = 0;

        while(s.hasNextDouble()){
            double d = s.nextDouble();
            m = m+1;
            sum = sum + d;
        }
        System.out.println(sum+" "+ sum/m);

        s.close();
    }
}
```

## 顺序结构
一句一句执行
## 选择结构
if单选/if双选/if多选/嵌套if/switch
```java
if(boolean){
boolean==true执行}
```
```java
package flow;

import javax.sql.rowset.spi.SyncResolver;
import java.util.Scanner;

public class Choice {
    public static void main(String[] args) {
        //单选
//        Scanner s = new Scanner(System.in);
//        String str = "qe";
//        String scanner = s.nextLine();
//        if (scanner.equals(str)){ //String的相等不能用'=='
//            System.out.println(scanner);
//        }
//        System.out.println("end");
//        s.close();

        //考试大于60ok 双选
//        Scanner scanner = new Scanner(System.in);
//        int score = scanner.nextInt();
//        if (score>60){
//            System.out.println("ok");
//        }else{
//            System.out.println("no");
//        }

        //多选
//        Scanner scanner = new Scanner(System.in);
//        int score = scanner.nextInt();
//        if (score==100){
//            System.out.println("100");
//        }else if (score<100 && score > 60){
//            System.out.println("yes");
//        }else if (score<60 && score > 0){
//            System.out.println("yes0");
//        }else{
//            System.out.println("buheguize");
//        }

        //switch case语句
//        反编译  java-class---反编译
        char grade = 'C';
//        String str = "laa"// 字符串也可以了
        switch (grade){
            case 'A':
                System.out.println("yes");
                break; //可选 如果下面不写，则会每个case挨个输出
            case 'C':
                System.out.println('u');
//            case 'laa':
//                System.out.println("str");
            default:
                System.out.println("ll");
        }

    }
}
```
## 循环结构
while / do ... while/  for  
大多数情况是会让循环停止下来，需要一个让表达式失效的语句
```java
package flow;

public class WhileTest {
    public static void main(String[] args) {
//        while
        int i = 0;
        int sum = 0;
//        while(i<101){
//            sum = sum+i;
//            i++;
//            System.out.println(sum);
//        }
        
//        do while 至少执行一次
        do{
            sum = sum+i;
            i++;
        }while(i<101);
        System.out.println(sum);
    }
}
```
## for循环
```java
for(initial; boolean; update){
\\code}
```
```java
package flow;

/*
最先执行的初始化步骤，可以声明一种类型，但可初始化一个或多个循环控制变量，也可以是空语句
检测布尔表达式值
执行一次循环后，更新循环变量
再次检测布尔表达式
 */

import java.util.Arrays;

public class ForFlow {
    public static void main(String[] args) {
//        int a = 1; //intial condition
//
//        while(a<101){ //判断条件
//            System.out.println(a); //循环体
//            a+=2;// a=a+2 迭代
//        }
//
//        //初始化；条件判断；迭代
//        for(int i = 1; i<101; i++){
//            System.out.println(i);
//        }
//        //100.for 自动生成上面的
//        for (;; ) {
//            //死循环
//        }
        //奇数偶数的和
//        int oddsum = 0;
//        int evensum = 0;
//        for (int i = 0; i < 100; i++) {
//            if (i%2 !=0){ //取模 奇数
//                oddsum+=i;
//            }else {
//                evensum+=i;
//            }
//        }
//        System.out.println(oddsum+" "+evensum);
        // while/for循环输出1-1000之间被5整除的数，并每行输出3个
//        int count = 0;
////        for (int i = 1; i < 1001; i++) {
////            if(i%5 == 0){
////                if (count<3){
////                    System.out.print(i+"\t"); // println 是每个输出就换行，print连续输出
////                    count+=1;
////                }else{
////                    System.out.println("\n");
////                    count = 0;
////                    System.out.print(i+"\t");
////                    count+=1;
////                }
////            }
////        }
//        int count = 0;
//        int i = 0;
//        while(i<101){
//            if(i%5==0){
//                if (count<3){
//                    System.out.print(i+"\t");
//                    count+=1;
//                }else{
//                    System.out.println();
//                    count=0;
//                    System.out.print(i+"\t");
//                    count+=1;
//                }
//            }
//            i++;
//        }
////        for (int i = 0; i < 1001; i++) {
////            if(i%5==0){
////                System.out.print(i+"\t");
////            }
////            if(i%(5*3)==0){
////                System.out.println("\n");
////            }
////        }
        //九九乘法表
        for (int i = 1; i < 10; i++) {
            for(int j = 1; j<=i;j++){
                System.out.print(i+"*"+j+"="+i*j+"\t");
            }
            System.out.println();
        }
    }
}
//增强for循环
        int[] num = {10,20,30,40};//定义一个数组
        for (int x: num){
            System.out.println(x);
        }
        for (int i = 0; i < 4; i++) {
            System.out.println(num[i]);
        }
```
## break continue
```java
        int i =0;
        while(i<100){
            i++;
//            if(i==30){
//                break;//强制退出
//            }
            if(i%10==0){
                System.out.println();
                continue; //终止某次，还能循环呢
            }
            System.out.println(i);
        }
	int count = 0;
        outer: for (int i = 101; i < 150; i++) {
            for(int j=2; j<i/2; j++){
                if(i%j ==0){
                    continue outer;
                }
            }
            System.out.println(i+" ");
        }
```
```java
//打印三角形 5行
        /*
0000*
000**1
00***11
0****111
*****1111
         */
        for (int i = 1; i <= 5; i++) {
            for(int j = 5; j>i; j--){
                System.out.print("0");
            }
            for(int j = 1; j<=i; j++){
                System.out.print("*");
            }
            for(int j = 1; j<i; j++){
                System.out.print("1");
            }
            //这个顺序执行的话，是在每行接着输出的呢！！！
            System.out.println();
        }
```
