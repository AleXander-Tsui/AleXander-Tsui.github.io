---
title: "AirSim在Linux下的安装"
data: 2019-6-29
categories: AirSim
tags:
- AirSim
- Linux
---

总结AirSim在Ububtu16.04下安装的相关问题。

<!-- more -->

## 介绍
**AirSim**是微软开发的用于多种仿真场景的软件，在自动驾驶、机器人、无人机等领域应用广泛，在我们之前的工作中，对小车的仿真多使用ROS自带的Gazebo，但有以下几点缺陷：
- 一台服务器只允许打开一个Gazebo。
- Gazebo速度慢，而且自建场景不方便。

所以我们想采用AirSim作为仿真工具，利用它提供的传感器，并利用ROS的接口调用它。

## 需求
首先明确我们要使用AirSim的哪些功能。
- 如果只是为了调用ROS的相关接口，使用其传感器信息，我们可以只用安装**AirSim**，具体按照<https://github.com/microsoft/AirSim/tree/master/ros/src/airsim_ros_pkgs>里面所写的做。
- 如果是为了使用完整的AirSim功能，就按照<https://github.com/microsoft/AirSim>所写的操作，需要安装UnrealEngine和AirSim。

## 注意点
1. 安装UnrealEngine需要先注册EpicGames账号，并关联你的github账号，才有获取源码的权限，才能进行安装。
2. 在测试ROS的接口时，我们可以使用tutorial中的程序进行测试。