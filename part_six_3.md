## 守护线程 daemon
线程分为用户线程和守护线程  
虚拟机必须确保用户线程执行完毕  
虚拟机不用等待守护线程执行完毕  
```java
package thread;

public class TestDaemon {
    public static void main(String[] args) {
        God god = new God();
        You1 you1 = new You1();

        Thread thread = new Thread(god);
        thread.setDaemon(true); //默认都是false用户线程，正常的线程都是用户线程

        thread.start(); //上帝守护线程
        // 守护线程不用管，只要用户线程完毕就停止
        new Thread(you1).start(); // 你 用户线程

    }
}

class God implements Runnable{
    @Override
    public void run() {
        while(true){
            System.out.println("shang di bao you ni ");
        }
    }
}


class You1 implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 8; i++) {
            System.out.println("happe");
        }
        System.out.println("nononononono");
    }
}
```

## 线程同步 synchronized
并发：同一个对象被多个线程同时操作  
多个线程访问同一个对象，并且某些线程还想改这个对象，这个时候需要线程同步，线程同步其实就是一种等待。  
**队列和锁**  
每个对象都有一个锁。  
一个线程持有锁或导致其他所有需要此锁的线程挂起。  
在多线程竞争下，加锁，释放锁会导致比较多的上下文切换和调度延时，引起性能问题  
如果一个优先级高的线程等待一个优先级低的线程释放锁会导致优先级倒置，引起性能问题。  

## 同步方法/同步块
由于我们可以通过private关键字来保证数据对象只能被方法访问，所以我们只需要针对方法提出一套机制，这套机制就是synchronized关键西。包含两种用法synchronized方法和synchronized块。  
synchronized 方法控制对’对象‘的访问，每个对象对应一把锁，每个synchronized方法必须获得带哦用该方法的对象的锁才能执行，否则线程阻塞，方法一旦执行，就独占该锁。知道该方法返回才释放锁，后面被阻塞的线程才能获得这个锁，继续执行。  
**同步块** synchronized（obj){}  
obj可以是任何对象，但是推荐使用共享资源作为同步监视器。  
里面放置的是需要**更改的代码**。  

## 死锁
多个线程各自占有一些共享资源，并且相互等待其他线程占有的资源才能运行，而导致两个或多个线程在等待对方释放资源，都停止执行的情形，某个拥有两个锁就有肯呢个发生。  
产生死锁的四个必要条件：  
互斥：一个资源每次只能被一个进程使用。  
请求与保持条件：一个进程因请求资源而阻塞时，对以获得的资源保持不妨。  
不剥夺条件：进程以获得的资源，在未使用完之前，不能强行剥夺。  
循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系。  
```java
package thread;

import java.util.concurrent.locks.ReentrantLock;

public class TestSynco {
    public static void main(String[] args) {
        BuyTicket station = new BuyTicket();
        new Thread(station,"1").start();
        new Thread(station,"2").start();
        new Thread(station,"3").start();
    }

}

class BuyTicket implements Runnable{
    private int tickernum=10;

    Boolean flag = true;

    private ReentrantLock lock = new ReentrantLock();

    @Override
    public void run() {
        while(flag){

            try {
                lock.lock(); //枷锁
                buy();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }finally {
                lock.unlock(); //解锁
            }
        }
    }
//同步方法，锁的是this/
    public  void buy() throws InterruptedException {
        if (tickernum<=0){
            flag=false;
            return;
        }

        Thread.sleep(1000);

        System.out.println(Thread.currentThread().getName()+"dd"+tickernum--);
    }

}

/*
1dd10
3dd9
2dd8
3dd6
1dd5
2dd7
1dd4
3dd2
2dd3
1dd1
3dd0
2dd-1  不安全又负数
 */
```
## 生产者消费者模式
生产者生成-放-仓库-消费者拿走。  
管城法/信号灯法/线程池  
1.继承Thread类  2.实现Runnable接口  3. 实现callable接口
```java 
import java.util.concurrent.Callable;
import java.util.concurrent.Future;
import java.util.concurrent.FutureTask;

public class Application {

    public static void main(String[] args) {
        mythread mythread = new mythread();
        mythread.start();

        Thread thread = new Thread(new myrunnable());
        thread.start();

        FutureTask futureTask = new FutureTask(new mycallable());
        new Thread(futureTask).start();
    }


}

class mythread extends Thread{
    @Override
    public void run() {
        super.run();
        System.out.println("THread");
    }
}

class myrunnable implements Runnable{
    @Override
    public void run() {
        System.out.println("runnable");
    }
}

class mycallable implements Callable{
    @Override
    public Object call() throws Exception {
        System.out.println("callanle");
        return null;
    }
}
```

