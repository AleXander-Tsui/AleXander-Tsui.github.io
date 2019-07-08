---
title: 向ORB-SLAM2的ROS包中添加自定义的消息
date: 2019-7-8
categories: ROS
tags:
- SLAM
- ROS
---

ORB-SLAM2向我们提供了ROS的接口，我们如何往其中添加自定义的消息呢？

<!-- more -->
## 目的
ORB-SLAM2提供了定位、生成相机位姿和轨迹的功能，但在建图任务中，我们需要实时获取相机的位姿（坐标和四元数）以及关键帧所对应的深度图，而在ORB-SLAM的源码中，其使用的都是ROS自带的消息类型，我们希望能自定义一个打包好图像ID（string）、深度图（sensor_msgs/Image）、相机位姿（数组或浮点数）的消息，实现实时publish该消息的功能。

## 尝试
最先的尝试是直接在`ORB-SLAM2/Examples/ROS/ORB_SLAM2`中新建`msg/`文件夹，加入所需消息，同时按要求修改`CMakeLists.txt`，然后编译，一切正常，`rosmsg show`也能显示自定义msg的信息，但在`ros_rgbd.cc`中试图publish该消息，却会报错:
```bash
Cannot load message class for .... Are your messages built?
```

## 解决方法
出现该错误的本质原因是因为没有将该自定义消息加入到ROS的空间中。编译正常，同时也能找到对应的头文件，但因为ORB-SLAM2的ROS包中`CMakeLists.txt`布局与一般的不同，同时缺少`package.xml`,编译也没有使用`catkin_make`，许多原因造成了ROS和该消息缺少了部分联系。  
解决办法就是在其它的包中按正常流程编译好消息，然后在ORB-SLAM2的源码中引用该头文件。具体需要修改的文件以及流程如下：
1. 在工作空间`catkin_ws/src`下新建一个功能包（或使用已有的功能包），在`msg/`中定义好需要的消息，按正常流程修改好`CMakeLists.txt`和`package.xml`，编译。
2. 修改`/catkin_ws/src/ORB_SLAM2/Examples/ROS/ORB_SLAM2/CMakeLists.txt`,在`include_directories`中加入1中编译好的消息头文件路径，我这里是`catkin_ws/devel/include`。
3. 修改`ros_rgbd.cc`，需要include该消息的头文件，即`rosmsg show`得到的地址。

最后编译ORB-SLAM，即可使用该消息了。

<img src="https://github.com/AleXander-Tsui/AleXander-Tsui.github.io/blob/master/images/avatar.jpeg" width=200>