# Using-SLAM-map-to-navigation
**_1. Install VMWare with ubuntu 18.04 and ROS Melodic._**

**_2. follow this steps._**

**_3. Open a terminal and use the following commands for installing ROS 1 on remote PC:_**
```
$ sudo apt-get update
$ sudo apt-get upgrade
$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_melodic.sh
$ chmod 755 ./install_ros_melodic.sh 
$ bash ./install_ros_melodic.sh
```
**_4. Install Dependent ROS 1 Packages:_**
```
$ sudo apt-get install ros-melodic-joy ros-melodic-teleop-twist-joy \
  ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc \
  ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan \
  ros-melodic-rosserial-arduino ros-melodic-rosserial-python \
  ros-melodic-rosserial-server ros-melodic-rosserial-client \
  ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server \
  ros-melodic-move-base ros-melodic-urdf ros-melodic-xacro \
  ros-melodic-compressed-image-transport ros-melodic-rqt* \
  ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers
```
**_5. Install TurtleBot3 Packages:_**
```
$ sudo apt-get install ros-melodic-dynamixel-sdk
$ sudo apt-get install ros-melodic-turtlebot3-msgs
$ sudo apt-get install ros-melodic-turtlebot3
```
**_6. Set TurtleBot3 Model Name:_**

_-In case of TurtleBot3 Burger_
```
$ echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
```
_-In case of TurtleBot3 Waffle Pi_
```
$ echo "export TURTLEBOT3_MODEL=waffle_pi" >> ~/.bashrc
```
**_7. Install Simulation Package:_**
```
$ cd ~/catkin_ws/src/
$ git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make
```
**_8. Launch Simulation World:_**
```
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
**_9. Run SLAM Node:_**
```
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
**_10. Operate TurtleBot3:_**

_In order to teleoperate the TurtleBot3 with the keyboard, launch the teleoperation node with below command in a new terminal window._
```
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

 Control Your TurtleBot3!
 ---------------------------
 Moving around:
        w
   a    s    d
        x

 w/x : increase/decrease linear velocity
 a/d : increase/decrease angular velocity
 space key, s : force stop

 CTRL-C to quit
```
**_11. When the map is created successfully, open a new terminal to save the map:_**
```
$ rosrun map_server map_saver -f ~/map
```
**_12. Run navigation node in a new terminal:_**
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```
**_13. Set Navigation Goal:_**

_1/ Click the "2D Nav Goal" button in the RViz menu._

_2/ Click on the map to set the destination of the robot and drag the green arrow toward the direction where the robot will be facing._

_"The Turtlebot should start moving to the destination."_
