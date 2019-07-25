---
title: AirSim仿真与ORB-SLAM、ROS结合使用
date: 2019-7-25
categories: ROS
tags:
- SLAM
- ROS
- AirSim
---

我们拥有一个AirSim仿真场景，ORB-SLAM的框架，以及ROS中的Gazebo、Rviz等可视化插件，如何启动一个导航仿真。

<!-- more -->
## 启动AirSim仿真场景
AirSim本质上是UnrealEngine中的一个插件，运行起来，实际上就是打开一个UnrealEngine工程，然后写好AirSim的配置文件，将AirSim插件添加进去，这样我们就会有一个场景，以及带有传感器的无人机或者小车。
按顺序如下：
- 打开UnrealEngine工程文件
- 配置好`settings.json`，可以模仿官方文档上的操作
```bash
$ source PATH_TO/AirSim/ros/devel/setup.bash
$ roscd airsim_tutorial_pkgs
$ cp settings/front_stereo_and_center_mono.json ~/Documents/AirSim/settings.json
```
- 按下UnrealEngine中的启动键，这时应该在仿真场景中会出现小车或无人机。
- 启动与ROS交互的AirSim节点，
```bash
$ roslaunch airsim_ros_pkgs airsim_node.launch
```
&emsp;&emsp; 这时`rostopic list`中应该就会有诸多传感器信息，比如深度图、RGB图或者激光雷达等信息。
- 启动无人机控制程序，为了在同一平面导航，先让无人机起飞，稳定在一个平面运动。

## 启动SLAM
直接`roslaunch`对应的SLAM文件，需要注意的是要`remap`一下RGB图和深度图的topic。

## 建图和导航
用键盘控制无人机运动，当出现`odom received`或者在Rviz中的Map的topic有3个话题时，建图完成，可以开始导航。
我们可以在Rviz中添加`PointCloud`、`TF`、`Path`，保证无人机与`projected map`在同一平面，用`2D Navigation`选定平面上一点，即可开始导航。