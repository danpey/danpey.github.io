# 创建用于arduino的消息类型

创建用于arduino的消息类型需要rosserial_arduino的包。通过这个包可以生成用于arduino的通信协议的头文件，可以使Arduino添加ROS节点，直接发布或订阅ROS消息。

## 安装
### apt-get安装
``` bash
sudo apt-get install ros-melodic-rosserial-arduino
sudo apt-get install ros-melodic-rosserial
```

### 源码安装
``` bash
cd <ws>/src
git clone https://github.com/ros-drivers/rosserial.git
cd <ws>
catkin_make
catkin_make install
```

## 添加到Arduino安装环境中
``` bash
cd <Arduino>/libraries
rosrun rosserial_arduino make_libraries.py .
```

然后即可看到所有的消息类型都已经生成在`ros_lib`文件中了。


参考网址：
[ROS学习之Arduino篇——rosserial_arduino包](https://blog.csdn.net/wanzew/article/details/80030768)



