## 多线程
程序，程序是指令和数据的有序集合，其本身没有任何运行含义，静态。  
进程，执行程序的一次执行过程，动态，是系统资源分配的单位。  
通常在一个进程中可以包含若干个线程，当然一个进程中至少有一个进程，不然没有存在的意义。线程是CPU调度和执行的单位。  
<p align="left">
  <Image src="pic/thread.png" width="739" height="466" />
</p>  

线程就是独立的执行路径；  
在程序运行时，即使没有自己创建线程，后台也会有多个线程，如主线程，gc线程；main（）称之为主线程，为系统的入口，用于执行整个程序；  
在一个进程中，如果开辟了多个线程，线程的运行由调度器安排调度，调度器是与操作系统紧密相关的，先后顺序是不能认为的干预的。  
对同一份资源操作时，会存在资源抢夺的问题，需要加入并发控制；  
线程会带来额外的开销，如cpu调度时间，并发控制开销。  
每个线程在自己的工作内存交互，内存控制不当会造成数据不一致  

## 创建1
<p align="left">
  <Image src="pic/chuangjian.png" width="656" height="308" />
</p>  

自定义线程类继承Thread类。  
重写run方法，编写线程执行体。  
创建线程对象，调用start方法启动线程。  
```java
class PrimeThread extends Thread {
         long minPrime;
         PrimeThread(long minPrime) {
             this.minPrime = minPrime;
         }

         public void run() {
             // compute primes larger than minPrime
              . . .
         }
     }
PrimeThread p = new PrimeThread(143);
     p.start();
```

```java
package thread;

//创建线程方法一：继承Thread类，重写run方法，调用start开启线程
//总结：注意，线程开启不一定立即执行，由CPU调度执行
public class MyThread extends Thread{
    @Override
    public void run() {
//        super.run();
        for (int i = 0; i < 5; i++) {
            System.out.println("zz" + i);
        }
    }

    public static void main(String[] args) {

        MyThread mt = new MyThread();
        mt.start();

        for (int i = 0; i < 5; i++) {
            System.out.println("ff" + i);
        }
    }
}

/*交替执行，如果调用run是先执行run，但是调用start的话交替执行
ff0
zz0
ff1
zz1
ff2
ff3
ff4
zz2
zz3
zz4
 */
```
```java
package thread;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;

//练习THread，实现多线程同步下载图片
public class MyThread2 extends Thread{

    private String url;
    private String name;

    public MyThread2(String url, String name) {
        this.url = url;
        this.name = name;
    }

    @Override
    public void run() {
//        super.run();
        WeDown weDown = new WeDown();
        weDown.downloader(url,name);
        System.out.println("kaishi "+name);
    }


    public static void main(String[] args) {
        MyThread2 myThread2 = new MyThread2("https://img2018.cnblogs.com/blog/1468796/201902/1468796-20190208222216724-198813524.png", "2.png");
        MyThread2 myThread3 = new MyThread2("https://img-blog.csdnimg.cn/20190530121245684.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNDExNTUw,size_16,color_FFFFFF,t_70", "3.png");
        
        //先2在3，理想的，顺序可能不是这个，代码是同时执行的
        myThread2.start();
        myThread3.start();
    }
}

class WeDown{
    //下载方法
    public void downloader(String url, String name){

        try {
            FileUtils.copyURLToFile(new URL(url), new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("IO异常");
        }
    }
}
```

## 创建2       
定义MyRunnable类实现Runnable接口  
实现run方法，编写线程执行体
创建线程对象，调用start方法启动线程  
```java
package thread;
//创建线程方法2：实现runnable接口，重写run，执行线程需要丢入runnable接口实现类，调用start
public class MyThread3 implements Runnable{
    @Override
    public void run() {
//        super.run();
        for (int i = 0; i < 5; i++) {
            System.out.println("zz" + i);
        }
    }

    public static void main(String[] args) {

//        第一种
//        MyThread mt = new MyThread();
//        mt.start();

        MyThread3 myThread3 = new MyThread3();
        Thread thread = new Thread(myThread3);
        thread.start();
        //上述可以简化为下面
//        new Thread(myThread3).start();

        for (int i = 0; i < 5; i++) {
            System.out.println("ff" + i);
        }
    }
}
/*
ff0
zz0
ff1
zz1
ff2
zz2
ff3
zz3
ff4
zz4
 */
```

<p align="left">
  <Image src="pic/chuangjian2.png" width="769" height="442.5" />
</p>  
 
继承Thread类  
  子类继承Thread类具备多线程能力  
  启动线程：子类对象.start()  
  不建议使用：**避免oop单继承的局限性**  
实现Runnable接口  
  实现接口Runnable具有多线程能力  
  启动线程：传入目标对象+Thread对象.start()  
  推荐使用：**灵活方便，方便同一个对象被多个线程使用**  
  
  
  
