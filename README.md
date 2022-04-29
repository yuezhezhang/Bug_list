# RosBug

To install [rosbash](http://wiki.ros.org/rosbash) (including command rosrun)
```
sudo apt-get install ros-noetic-rosbash
```

To install turtlesim
```
sudo apt-get install ros-noetic-turtlesim
```
Run the following commands in three terminals
```
roscore
rosrun turtlesim turtlesim_node
rosrun turtlesim turtle_teleop_key
```

Rolaunch cannot find some package, the reason could be the package has not been installed such as turtlesim, or not ```source devel/setup.bash```

To install [xacro](http://wiki.ros.org/xacro)  (useful when working with large XML documents such as robot descriptions. It is heavily used in packages such as the urdf.)
```
sudo apt-get install ros-noetic-xacro
```

Robot state publisher error
```
sudo apt-get install ros-noetic-robot-state-publisher
```

Install [rviz](http://wiki.ros.org/rviz/UserGuide)
```
sudo apt-get install ros-noetic-rviz
```
