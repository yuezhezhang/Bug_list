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
