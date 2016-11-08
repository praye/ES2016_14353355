###Ubuntu 14.04安装ROS
1.配置Ubuntu要求允许接受"restricted," "universe," and "multiverse."的软件源,可以根据[这个链接](https://help.ubuntu.com/community/Repositories/Ubuntu)来进行配置。  
PS：好像默认配置就是这个，可以不用配置。  

2.设置sources.list（软件源）:  

    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
3.设置密钥：  

    sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
4.安装：  
首先确认你的Debian的软件包索引是最新的:  

    sudo apt-get update
在ROS中有许多不同的函数库和工具,建议是完全安装。  
我这里选择完全安装。

    sudo apt-get install ros-indigo-desktop-full

5.初始化rosdep：  

    sudo rosdep init
    rosdep update

6.设置环境  
添加ROS的环境变量,这样,当你打开你新的shell时,你的bash回话中会自动添加环境变量。  

    echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
    source ~/.bashrc

7.安装rosinstall：  

    sudo apt-get install python-rosinstall
