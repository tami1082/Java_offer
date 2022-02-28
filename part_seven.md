## 文件
输入流：文件-代码  
输出流：代码-文件  
创建文件对象相关构造器和方法  
```java
package file;

import java.io.File;
import java.io.IOException;

public class TestFile {
    public static void main(String[] args) throws IOException {
        TestFile testFile = new TestFile();
        String path = "D:\\0_daily\\Temp\\java\\code\\pro_empty\\1.txt";
        testFile.c1(path);

        String par = "D:\\0_daily\\Temp\\java\\code\\pro_empty";
        String son = "\\2.txt";
        testFile.c2(par,son);

    }

    //根据路径创建一个file对象
    public void c1(String pathname) throws IOException {
        //这个new时在内存上，只是在Java程序中，只是对象
        File file = new File(pathname);
        //执行这个才是真正的写入
        file.createNewFile();
    }
    //根据父目录文件+子路径构建
    public void c2(String par, String son) throws IOException {
        File file = new File(par+son);
        file.createNewFile();
    }

}
```
## 获取文件信息
```java

    //获取文件信息
    public void info(){
        //先创建文件对象
        File file = new File("D:\\0_daily\\Temp\\java\\code\\pro_empty\\1.txt");
        System.out.println("wenjianwen "+file.getName());
    }

    //getName, getAbsolutePath getParent length exist isFile isDirectory
```
```java
//mkdir 创建一级目录 mkdirs创建多级目录 delete删除空目录或文件
    public void info(){
        //先创建文件对象
        File file = new File("D:\\0_daily\\Temp\\java\\code\\pro_empty\\1.txt");
//       File file = new File("D:\\0_daily\\Temp\\java\\code\\pro_empty");
        if (file.exists()){
            file.delete();
            System.out.println("ok shan");
        }else{
//           if (file.mkdirs()){
//                 System.out.println("oook");
//             }
            System.out.println("shibai ");
        }
//        System.out.println("wenjianwen "+file.getName());
    }
```
## IO流原理及流
Java中，对于数据的输入/输出操作以“Stream”的方式进行，Java.io包下提供了各种“流”的接口和类。  
|抽象基类|字节流|字符流|
|--|--|--|
||8bit|按字符|
|输入流|InputStream|Reader|
|输出流|OutputStream|Writer|
