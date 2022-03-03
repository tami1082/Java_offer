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

## FileInputStream
InputStream:字节输入流，抽象类是所有类字节输入流的超类。  
InputStream 常用子类：FileInputStream 文件输入流，BufferedInputStream：缓冲字节输入流，ObjectInputStream：对象字节输入流  
```java
package file;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class TestFile {
    public static void main(String[] args) throws IOException {
        TestFile testFile = new TestFile();
        testFile.readFile();
    }

    public void readFile() throws IOException {
        String Filepath = "D:\\0_daily\\Temp\\java\\code\\pro_empty\\2.txt";
        int read2 = 0;
        FileInputStream fileInputStream = new FileInputStream(Filepath); //用于读取文件
        //返回-1表示读完了
        while((read2 = fileInputStream.read()) != -1){
            System.out.println((char)read2);
        }; //如果返回-1表示读完了
        fileInputStream.close();
    }
/*
w
e


s
d
a
f

 */

    public void readFile2() throws IOException {
        String Filepath = "D:\\0_daily\\Temp\\java\\code\\pro_empty\\2.txt";
        int read2 = 0;
        byte[] buf = new byte[4];//一次读8个字节
        FileInputStream fileInputStream = new FileInputStream(Filepath); //用于读取文件
        //返回-1表示读完了 这个read2是实际返回的读取的长度
        while((read2 = fileInputStream.read(buf)) != -1){
            System.out.println(new String(buf,0,read2));
        }; //如果返回-1表示读完了
        fileInputStream.close();
    }
    /*
    we
    sdaf
     */

}
```

## FileOutputStream
这个是写入，会在文件不存在时候，创建文件，前提是目录已经存在了。  
```java
package file;

import java.io.*;
import java.nio.charset.StandardCharsets;

public class TestFile {
    public static void main(String[] args) throws IOException {
        TestFile testFile = new TestFile();
        testFile.writeFile();
    }

    public void writeFile() throws IOException {
        String path = "D:\\0_daily\\Temp\\java\\code\\pro_empty\\a.txt";
        //下面这种写入是会覆盖写入的
        //new FileOutputStream(path,true);这样是追加写入不是覆盖啦
        FileOutputStream fileOutputStream = new FileOutputStream(path);
        //写入一个字节
        fileOutputStream.write('a');
        //写入字符串
        String str = "lao zhang ai wo";
        //str.getBytes() 可以把 字符串->字节数组
        fileOutputStream.write(str.getBytes(StandardCharsets.UTF_8));
        //写入固定的长度的东西
        fileOutputStream.write(str.getBytes(StandardCharsets.UTF_8),0,str.length());
        
        fileOutputStream.close();
    }
}
```

## 文件拷贝
```java
package file;

import java.io.*;
import java.nio.charset.StandardCharsets;

public class TestFile {
    public static void main(String[] args) throws IOException {
        TestFile testFile = new TestFile();
        testFile.writeFile();
    }

    public void writeFile() throws IOException {
        String ipath = "D:\\0_daily\\Temp\\java\\code\\pro_empty\\2.png";
        String opath = "D:\\0_daily\\Temp\\java\\code\\pro_empty\\basis_language\\2.png";
        // 在完成程序时，应该时读取部分数据就写，度一点写一点
        FileInputStream fileInputStream = new FileInputStream(ipath);
        FileOutputStream fileOutputStream = new FileOutputStream(opath);
        //1 创建文件的输入流，将文件读入到程序
        //2.创建文件的输出流，将读取到的文件数据，写入到指定的文件
        byte[] buf = new byte[1024];
        int readlen = 0;
        while((readlen = fileInputStream.read(buf)) != -1){
            fileOutputStream.write(buf,0,readlen); //一定要这样控制读入的长度，万一不够长
        }
        System.out.println("ok");

        //如果流有使用 就关闭！
        if (fileInputStream != null){
            fileInputStream.close();
        }
        if (fileOutputStream != null){
            fileOutputStream.close();
        }
    }
}
```

