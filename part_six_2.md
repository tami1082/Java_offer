## 静态代理
```java
package thread;
/*
真实对象和代理对象都要实现同一个接口
代理对象要代理真实角色
代理对象可以做很多真实对象做不了的，真实线程比较专注
 */
public class StaticAg {

    public static void main(String[] args) {
        new Thread(()-> System.out.println("love")).start();

        Agent agent = new Agent( new You() );
        agent.happyMarry();
    }
}

interface Marry{
    void happyMarry();
}

class You implements Marry{
    @Override
    public void happyMarry() {
        System.out.println("happy");
    }
}

class Agent implements Marry{
    //代理真实目标角色
    private Marry target;

    public Agent(Marry target) {
        this.target = target;
    }

    @Override
    public void happyMarry() {
        before();
        this.target.happyMarry();
        after();
    }

    private void after() {
        System.out.println("buzhi");
    }

    private void before() {
        System.out.println("weikuan");
    }
}
```

## lamda表达式
避免匿名内部类定义过多  
functional interface函数式接口  
定义：任何接口，如果只包含**唯一**一个抽象方法，那么它就是一个函数式接口；对于函数式接口，我们可以通过lambda表达式创建该接口的对象。  
```java
public interface Runnable{
  public abstract void run();
}```

```java
package thread;

public class TestLambda {
    //静态内部类
    static class Like2 implements iLike{
        @Override
        public void lambda() {
            System.out.println("lambd222a");
        }
    }

    public static void main(String[] args) {
        Like iLike = new Like();
        iLike.lambda();

        Like2 like = new Like2();
        like.lambda();

        //局部内部类
        class Like3 implements iLike{
            @Override
            public void lambda() {
                System.out.println("lamb3333da");
            }
        }
        Like3 like3 = new Like3();
        like3.lambda();


        //匿名内部类，没有类的名称，必须借助接口或父类
        iLike like4 = new iLike() {
            @Override
            public void lambda() {
                System.out.println("44444");
            }
        };
        like4.lambda();

        //lambda
        iLike like5 = () -> {
            System.out.println("5555");
        };
        like5.lambda();
    }

}

//定义一个函数式接口
interface iLike{
    void lambda();
}

////实现类
class Like implements iLike{
    @Override
    public void lambda() {
        System.out.println("lambda");
    }
}
```

