# RosBug

1. To install [rosbash](http://wiki.ros.org/rosbash) (including command rosrun)
```
sudo apt-get install ros-noetic-rosbash
```

2. To install turtlesim
```
sudo apt-get install ros-noetic-turtlesim
# Run the following commands in three terminals
roscore
rosrun turtlesim turtlesim_node
rosrun turtlesim turtle_teleop_key
```

3. Rolaunch cannot find some package, the reason could be the package has not been installed such as turtlesim, or not ```source devel/setup.bash```

4. To install [xacro](http://wiki.ros.org/xacro)  (useful when working with large XML documents such as robot descriptions. It is heavily used in packages such as the urdf.)
```
sudo apt-get install ros-noetic-xacro
```

5. Robot state publisher error
```
sudo apt-get install ros-noetic-robot-state-publisher
```

6. Install [rviz](http://wiki.ros.org/rviz/UserGuide)
```
sudo apt-get install ros-noetic-rviz
```

7. Can not use python multiprocessing in ROS **--remaining issue**
* [stackoverflow link](https://stackoverflow.com/questions/70968015/cant-use-pool-map-for-a-class-method-in-ros-python)
* [pickle](https://docs.python.org/3/library/pickle.html#what-can-be-pickled-and-unpickled)
* [ParallelProcessing](https://wiki.python.org/moin/ParallelProcessing)

8. Git submodule 
* [easy way to pull all submodules](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)
* [common code already exists in the index](https://stackoverflow.com/questions/12898278/issue-with-adding-common-code-as-git-submodule-already-exists-in-the-index)
* [some steps](https://www.jianshu.com/p/9000cd49822c)
* [git submodule push](https://stackoverflow.com/questions/5814319/git-submodule-push/10878273#10878273)
* [push submodule to remote](https://stackoverflow.com/questions/8372625/git-how-to-push-submodule-to-a-remote-repository)
* [how to push third party code to my repository](https://segmentfault.com/a/1190000009928515) **--remaining issue**
