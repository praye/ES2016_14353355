## DOL开发环境配置
###DOL是什么
The distributed operation layer (DOL) is a framework that enables the (semi-) automatic
mapping of applications onto the multiprocessor SHAPES architecture platform. The DOL
consists of basically three parts:  
**DOL Application Programming Interface**  
**DOL Functional Simulation**  
**DOL Mapping Optimization**  

### 配置DOL
本次实验环境为Linux，我是在虚拟机中的Ubuntu上进行配置的
#### 首先要安装一下必要的环境
    sudo apt-get update
    sudo apt-get install ant
    sudo apt-get install openjdk-7-jdk
    sudo apt-get install unzip

#### 下载文件
两个文件分别是systemc-2.31.tgz和dol_ethz.zip。  
下载有可能会失败，有可能要多试几次。  
如果你在Windows里下载好，可以自行拉进虚拟机中，不用进行这个下载的步骤。

    sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
    
    sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

#### 解压文件
新建dol文件夹

    mkdir dol
将dolethz.zip解压到 dol文件夹中
    
    unzip dol_ethz.zip -d dol
解压systemc

    tar -zxvf systemc-2.3.1.tgz

#### 编译systemc
解压后进入systemc-2.3.1的目录下

    cd systemc-2.3.1
新建一个临时文件夹objdir并进入该文件夹

    mkdir objdir
    cd objdir
运行configure(能根据系统的环境设置一下参数，用于编译)

    ../configure CXX=g++ --disable-async-updates
能看到这个步骤的截图如下：

![](http://p1.bqimg.com/4851/45a97cafa9b4f1a1.jpg)

编译

    sudo make install
编译后文件目录如下

    cd ..
    ls
![](http://p1.bqimg.com/4851/a3f19809b14ee13a.jpg)  

记录当前的工作路径(会输出当前所在路径，记下来，待会有用)

    pwd
![](http://i1.piimg.com/4851/378e9b1c6d0b00a9.jpg)  
这是我当前的文件路径。  

#### 编译dol
进入刚刚dol的文件夹

    cd ../dol
修改build_zip.xml文件
找到下面这段话，就是说上面编译的systemc位置在哪里，  

**\<property name="systemc.inc" value="YYY/include"/>  
\<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>**

把YYY改成上页pwd的结果（注意，对于64位系统的机器，lib-linux要改成lib-linux64）  

然后是编译

    ant -f build_zip.xml all
若成功会显示build successful,如下图

![](http://p1.bpimg.com/4851/c235dcf28ca9d069.jpg)  

接着可以试试运行第一个例子  

进入build/bin/main路径下

    cd build/bin/main
运行第一个例子

    ant -f runexample.xml -Dnumber=1
成功结果如图

![](http://p1.bpimg.com/4851/f9e50079393bb7c8.jpg)

#### 至此，整个配置过程完成
