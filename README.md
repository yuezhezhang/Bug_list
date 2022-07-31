# Ros bug list

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

## Singularity
1. [To create the singularity image](https://github.com/yuezhezhang/discrete_active_inference/tree/main/singularity_environment)
2. [Add dependencies to the singularity](https://people.tuebingen.mpg.de/felixwidmaier/rrc2021/singularity.html#add-custom-dependencies-to-the-container)

## Latex
1. [Cite range of papers](https://tex.stackexchange.com/questions/3871/citing-a-range-of-papers-using-numeric-keys-as-in-citea-b-c-1-3)
```
\documentclass{article}
\usepackage[style=numeric-comp]{biblatex}
\bibliography{xampl}
\begin{document}
hello \cite{article-full,book-full,mastersthesis-full}
\printbibliography
\end{document}
```
2. [Mathematical symbols](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)

3. [Adjust width of algorithm](https://tex.stackexchange.com/questions/350434/adjust-width-of-algorithm-float)

4. [Add section without number to the table of content](https://tex.stackexchange.com/questions/30122/generate-table-of-contents-when-section-sections-without-numbering-has-been)
* If we donot want to keep the traditional numbered space
   ```
   \chapter{Glossary}

   \section*{List of Abbreviations}
   \addcontentsline{toc}{section}{List of Abbreviations}%

   \section*{List of Symbols}
   \addcontentsline{toc}{section}{List of Symbols}%
   ```
   ![fig](https://github.com/yuezhezhang/ROS_bug_list/blob/main/images/latex-4-1.png)
* If we want to keep the traditional numbered space
   ```
   \chapter{Glossary}

   \section*{List of Abbreviations}
   \addcontentsline{toc}{section}{\protect\numberline{}List of Abbreviations}%
   
   \section*{List of Symbols}
   \addcontentsline{toc}{section}{\protect\numberline{}List of Symbols}%
   ```
   ![fig](https://github.com/yuezhezhang/ROS_bug_list/blob/main/images/latex-4-2.png)

## Git collaboration
1. Git submodule 
* [easy way to pull all submodules](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)
* [common code already exists in the index](https://stackoverflow.com/questions/12898278/issue-with-adding-common-code-as-git-submodule-already-exists-in-the-index)
* [some steps](https://www.jianshu.com/p/9000cd49822c)
* [git submodule push](https://stackoverflow.com/questions/5814319/git-submodule-push/10878273#10878273)
* [push submodule to remote](https://stackoverflow.com/questions/8372625/git-how-to-push-submodule-to-a-remote-repository)
* [how to push third party code to my repository](https://segmentfault.com/a/1190000009928515) **-- remaining issue**

## Tutorials
1. [ROS tutorials](http://wiki.ros.org/ROS/Tutorials)
2. [URDF](http://wiki.ros.org/urdf) is a package containing a C++ parser for the Unified Robot Description Format (URDF), which is an XML format for representing a robot model. 
3. [rqt](http://wiki.ros.org/rqt) is a software framework of ROS that implements the various GUI tools in the form of plugins.
4. [Navigation sending simple goals](http://library.isr.ist.utl.pt/docs/roswiki/navigation%282f%29Tutorials%282f%29SendingSimpleGoals.html)

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

4. [ROSPlan change planner](https://github.com/KCL-Planning/ROSPlan/issues/13)
5. [ROSPlan planner interface](https://kcl-planning.github.io/ROSPlan//documentation/interfaces/02_planner_interface.html)

## Issac Gym
1. Find isaac gym here https://developer.nvidia.com/isaac-gym. Register and download the simulator.  Within the download, there is a folder called 'docs'. Follow the instructions

2. Install in a new conda environment (In the root directory)
```
./create_conda_env_rlgpu.sh
```
3. Activate by running
```
conda activate rlgpu
```
4. Deactivate by running
```
conda deactivate
```
5. Install Example RL Environments
Visit https://github.com/NVIDIA-Omniverse/IsaacGymEnvs and follow the setup instructions in the README.

6. Trouble shooting
* Error `ImportError: libpython3.7m.so.1.0: cannot open shared object file: No such file or directory`
* Set the LD_LIBRARY_PATH variable in rlgpu environment (should be updated every time) 
   ```
   export LD_LIBRARY_PATH=/home/zyz/anaconda3/envs/rlgpu/lib
   ```
* Then run the simple example would be fine.
* We can `echo $PATH` in different conda environment
