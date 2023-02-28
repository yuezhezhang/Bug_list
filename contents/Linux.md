## Linux commands
1. Open tty4
* `Ctrl + Alt + F4`

2. View the log of dpkg installation
* `vim /var/log/dpkg.log`

3. Take a screenshot
* `Shift + prtsc`

4. [To fold file in VSCode (e.g. xml file)](https://blog.csdn.net/wuyujin1997/article/details/108424032)
* `Ctrl + K + 0` 

5. Open another terminal 
* `Ctrl + shift + K`

6. To change the background colour in VSCode
* `Ctrl + K + T`

7. [Find the Process ID of a program and kill it](https://itsfoss.com/how-to-find-the-process-id-of-a-program-and-kill-it-quick-tip/)
```
ps aux | grep -i “name of program”
sudo kill -9 process_id
```
8. [Rosclean](http://wiki.ros.org/rosclean)
* rosclean will cleanup filesystem resources, such as log files
* `rosclean check`
* `rosclean purge`

8. [Screenshot with dimensions](https://askubuntu.com/questions/262253/how-do-i-take-a-screenshot-with-dimensions)
* Use "shutter"

9. Video recording
* Use [OBS](https://obsproject.com/)
* Use [Kazam](https://itsfoss.com/kazam-screen-recorder/)

10. [Top command weird characters](https://stackoverflow.com/questions/30999873/output-of-top-command-contains-weird-characters)
```
top -cb | grep "dus_static" > cpu_info.txt
```

## Installation
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

8. [Black sgreen due to sogopinyin](https://blog.csdn.net/Mr_Cat123/article/details/78573780)
```
Ctrl + Alt + F4
sudo apt-get purge sogoupinyin
sudo apt-get purge fcitx
sudo apt-get autoremove
reboot 
```

## Update
1. update
```
sudo apt update 
```
2. check upgradable list
```
apt list --upgradable | grep google
```
3. [update google](https://itsfoss.com/update-google-chrome-ubuntu/) 
```
sudo apt --only-upgrade install google-chrome-stable
```


## Singularity
1. [To create the singularity image](https://github.com/yuezhezhang/discrete_active_inference/tree/main/singularity_environment)
2. [Add dependencies to the singularity](https://people.tuebingen.mpg.de/felixwidmaier/rrc2021/singularity.html#add-custom-dependencies-to-the-container)
