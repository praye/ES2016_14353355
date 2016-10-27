##死锁
###先来一个例子
Deadlock.java文件如下：  

    class A{
      synchronized void methodA(B b){
    b.last();
      }
      synchronized void last(){
    System.out.println("Inside A.last()");
      }
    }
    class B{
      synchronized void methodB(A a){
    a.last();
      }
      synchronized void last(){
    System.out.println("Inside B.last()");
      }
    }
    class Deadlock implements Runnable{
      A a = new A();
      B b = new B();
      Deadlock(){
    Thread t = new Thread(this);
    int count = 20000;
    t.start();
    while(count -- > 0);
    a.methodA(b);
      }
    public void run(){
      b.methodB(a);
    }
    public static void main(String args[]){
      new Deadlock();
    }
    }
用Java的IDE或者用javac来编译  
用javac的命令行如下:

    javac Deadlock.java	
linux系统或者Windows系统下编写bat文件，放下和编译产生的Deadlock.class同一个目录下
bat文件如下:

    cd /d %~dp0
    @echo off
    :start
    set /a var+=1
    echo %var%
    java Deadlock
    if %var% leq 1000 GOTO start
    pause
双击运行，可以发现发生死锁。  
我是在Windows系统下运行的，可以看到死锁发生了。  
![](https://ooo.0o0.ooo/2016/10/27/58118b9646e33.png)  
  
###我们知道，死锁的发生需要四个必要条件：  
*互斥条件：一个资源每次只能被一个进程使用  
请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放  
不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺  
循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系*

####所以我们看看上面的程序为什么会发生死锁
新建线程t被调度的时候，就会执行run()里面的代码，即调用a的last()，而主线程恰好执行a.methoA(b)的时候，需要执行b.last()。我们发现A和B两个类的方法都用了关键字synchronized来修饰。  
所以主线程和线程t都会因为没有得到资源而阻塞，等待对方执行完成，产生了死锁。  
###关键字 synchronized:   
*当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。  
当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。*
