# WPR系列机器人仿真工具

## 准备工作

1. 安装ROS桌面完整版(Kinetic/Ubuntu 16.04):
```
sudo apt-get install ros-kinetic-desktop-full
```
由于Indigo/Ubuntu 14.04集成的Gazebo版本太过古老，所以无法进行支持，建议升级到Kinetic/Ubuntu 16.04。

2. 获取源码:
```
cd ~/catkin_ws/src/
git clone https://github.com/6-robot/wpr_simulation.git
```
3. 编译
```
cd ~/catkin_ws
catkin_make
```

## 使用说明

### 1. 启智ROS机器人
简单场景:
```
roslaunch wpr_simulation wpb_simple.launch
```
![wpb_simple pic](./media/wpb_simple.png)

SLAM环境地图创建:
```
roslaunch wpr_simulation wpb_gmapping.launch
```
![wpb_gmapping pic](./media/wpb_gmapping.png)

Navigation导航:
```
roslaunch wpr_simulation wpb_navigation.launch
```
![wpb_navigation pic](./media/wpb_navigation.png)

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)