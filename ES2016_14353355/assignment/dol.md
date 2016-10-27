##DOL实例分析&编程
###这次的任务有两个：
1. 修改example2，让3个square模块变成2个, tips:修改xml的iterator
2. 修改example1，使其输出3次方数，tips:修改square.c
####其实我们应该先来看example里面各文件是什么东东（TA说的）
src文件夹：各进程（生产者，消费者，处理模块等）的功能定义  
example1.xml：系统架构即模块连接方式定义  

![](https://ooo.0o0.ooo/2016/10/26/5810c8c492728.png)  

src 文件夹内包含2种文件：.c, 与对应的.h，就是实现的模块，就是.dot的框框的功能描述。（每个模块要实现2个接口，xxx_init和xxx_fire两个函数，分别是初始化这个模块是干了什么，以及这个模块开干的时候做什么）  
###然后开干吧
###第一个任务是修改example2
![](https://ooo.0o0.ooo/2016/10/26/5810c0b6da6c7.png)  
没错，就是把光标那里的3改成2,就成了。
 
####运行结果  
2表示example2，如果之前编译运行过要在\dol\bin\main里删掉相应的文件夹  

    cd dol/build/bin/main
    sudo ant –f runexample.xml –Dnumber=2

  
![](https://ooo.0o0.ooo/2016/10/26/5810c0b6e5315.png)  

####来看看dot图，果然成了两个  
![](https://ooo.0o0.ooo/2016/10/26/5810c0b6da43e.png) 
  
##
###第二个任务是修改example1  
同样，这个也只需要修改一个地方就好了，看到光标的地方没有，输出3次方数，再多乘一个i不就得了？  

![](https://ooo.0o0.ooo/2016/10/26/5810d0c100c13.png)

###运行结果
同样，1表示example1，如果之前编译运行过要在\dol\bin\main里删掉相应的文件夹   

    sudo ant –f runexample.xml –Dnumber=1

![](https://ooo.0o0.ooo/2016/10/26/5810d469d6329.png)

####看看dot图
![](https://ooo.0o0.ooo/2016/10/26/5810d469cb6b0.png)  

###为什么要这样改呢
example1就不用说啦，平方改成3次方，多乘一次i就好了  
而在example2.xml中定义了生产者模块、迭代产生3（就在截图代码里光标的位置）个平方模块、消费者模块，每个模块之间通过sw_channel连接，因此，要产生2个square模块，将迭代的次数N改为2即可。

###实验感想
其实这次实验还是比较多的不懂，虽然说大致看了一下代码，知道要怎么改，但对于很多概念性的问题还是不明白，还需要加强看代码的能力。  
PS：上次用的一个图床似乎不怎么好用，这次改成了[SM.MS](https://sm.ms)，觉得还不错。