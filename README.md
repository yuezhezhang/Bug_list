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

rolaunch cannot find some package, the reason could be the package has not been installed such as turtlesim, or not ```source devel/setup.bash```
