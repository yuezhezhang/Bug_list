# Ros bug list

## Installation and Linux commands
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

7. Rospack cannot find installed package
* [the reason could be](https://blog.csdn.net/scx837685002/article/details/78249961)
* [solution](https://stackoverflow.com/questions/27053334/ros-package-not-found-after-catkin-make)

## Singularity
1. [To create the singularity image](https://github.com/yuezhezhang/discrete_active_inference/tree/main/singularity_environment)

## Git collaboration
1. Git submodule 
* [easy way to pull all submodules](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)
* [common code already exists in the index](https://stackoverflow.com/questions/12898278/issue-with-adding-common-code-as-git-submodule-already-exists-in-the-index)
* [some steps](https://www.jianshu.com/p/9000cd49822c)
* [git submodule push](https://stackoverflow.com/questions/5814319/git-submodule-push/10878273#10878273)
* [push submodule to remote](https://stackoverflow.com/questions/8372625/git-how-to-push-submodule-to-a-remote-repository)
* [how to push third party code to my repository](https://segmentfault.com/a/1190000009928515) **-- remaining issue**


## Coding
1. Can not use python multiprocessing in ROS **-- remaining issue**
* [stackoverflow link](https://stackoverflow.com/questions/70968015/cant-use-pool-map-for-a-class-method-in-ros-python)
* [pickle](https://docs.python.org/3/library/pickle.html#what-can-be-pickled-and-unpickled)
* [ParallelProcessing](https://wiki.python.org/moin/ParallelProcessing)

2. Action server with multiple goals **-- remaining issue**
* [action server with more than one action](https://answers.ros.org/question/9776/action-server-with-more-than-one-action/)
* [how to handle multiple goals with Action API (without waitForResult )](https://answers.ros.org/question/292507/how-to-handle-multiple-goals-with-action-api-without-waitforresult/)
* [sending a sequence of goals to move_base](https://answers.ros.org/question/210987/sending-a-sequence-of-goals-to-move_base/)
* [how to send multiple goals with actionlib and c++](https://answers.ros.org/question/361326/how-to-send-multiple-goals-with-actionlib-and-c/)
* [action lib detailed description](http://wiki.ros.org/actionlib/DetailedDescription) 
* simple action server can not handle multiple goals.If I send 5 goals, it cancels the 2, 3, 4 goals.

3. Executing multiple tasks simultanuously
* [discuss](https://github.com/ros-planning/moveit/pull/2810)
* [draft](https://github.com/ros-planning/moveit/pull/2810)

## Others
1. [To fold file in VSCode (e.g. xml file)](https://blog.csdn.net/wuyujin1997/article/details/108424032)
* Ctrl + K + 0 

