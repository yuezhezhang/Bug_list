## Installation

* follow the installation steps in [robotic](https://github.com/MarcToussaint/robotic/tree/a9adb1b50cca67e614f88481371bb7d76ba0c25a), especially from **Installation from source with real Franka**
* install physx error, fix this by [see](https://stackoverflow.com/questions/26380407/cmake-clang-is-not-able-compile-a-simple-test-program-fedora-20)
  ```
  sudo apt install libstdc++-12-dev
  ```
* can not find glm headers, [see](https://stackoverflow.com/questions/28977455/why-cant-c-find-glm-headers)
  ```
  sudo apt-get install libglm-dev
  ```
* can not find lANN
  ```
  sudo apt-get install libann-dev
  ./install.sh libann
  ```
* to disable pybind in CMakeLists.txt of botop
  ```
  option(USE_PYBIND "build python bindings" OFF)

  # or in the terminal
  # cmake -DUSE_PYBIND=OFF -DUSE_BULLET=OFF -DUSE_OPENCV=OFF -DPY_VERSION=$PY_VERSION . -B build 

  if(USE_PYBIND)
    add_custom_target(docstrings #ALL
      DEPENDS _robotic
      COMMAND env PYTHONPATH="." pybind11-stubgen --ignore-all-errors _robotic
      COMMAND mv stubs/_robotic*/__init__.pyi _robotic.pyi
      COMMAND mv stubs/_robotic*/*.pyi .)
  endif()

  if(USE_PYBIND)
    message(STATUS "[rai] installing python packages in " ${PY_LIB_SITE}/robotic )
  
    install(
      TARGETS _robotic
      DESTINATION ${PY_LIB_SITE}/robotic)
  
    install(
      DIRECTORY rai-robotModels
      DESTINATION ${PY_LIB_SITE}/robotic
      FILES_MATCHING
      PATTERN "*.g" PATTERN "*.ply"
      PATTERN "retired" EXCLUDE
      )
  endif()
  ```
* current robotic version 1.10 and update its submodule
  ```
  git reset --hard 0d246d1ecd84aa308eb78622b20193dc9db70969
  git submodule update --recursive
  ```
* update rai version
  ```
  cd rai  
  git reset --hard 8547d4380a2c5169f63d6fe18b6d234143cc59c4
  ```
* for display current commit version
  ```
  git rev-parse HEAD
  ```
* update franka ip `192.168.2.55` in `robotic/botop/src/Franka/franka.cpp` and `FrankaGripper.cpp`
* compile
  ```
  cd robotic
  # rm -rf build # if needed 
  export PY_VERSION=`python3 -c "import sys; print(str(sys.version_info[0])+'.'+str(sys.version_info[1]))"`
  cmake -DPY_VERSION=$PY_VERSION -DUSE_REALSENSE=OFF -DUSE_LIBFRANKA=ON . -B build
  make -C build _robotic install

  export PATH="$HOME/.local/bin:$PATH"
  ry-bot -real -up -home
  ```

## Apollo Installation 
* install [libfranka0.14.0](https://github.com/frankaemika/libfranka/blob/main/README.md) under ```~/git/``` , and also needs to install [pinocchio](https://stack-of-tasks.github.io/pinocchio/download.html)
* After installed libfranka, change the libfranka version to "0.14.0" in ```git/install.sh```, and then run ```./install.sh libfranka``` , when installing robotic. robot server version 8, should install libfranka 0.14.0, [see](https://frankaemika.github.io/docs/compatibility.html)

* add the following limits to the realtime group in ```/etc/security/limits.conf```
```bash
@realtime soft rtprio 99
@realtime soft priority 99
@realtime soft memlock 102400
@realtime hard rtprio 99
@realtime hard priority 99
@realtime hard memlock 102400
```

## Demeter, Apollo, and Athena
* PC login: irosa-komo123
* ip: 10.10.10.10, 9.9.9.9
* usrname: admin
* password: RZWjZAwtCzUFAgj 


## Setup for dual panda(Demeter and Apollo)

* update franka ip `192.168.2.55` , `10.10.10.10` in `robotic/botop/src/Franka/franka.cpp` and `FrankaGripper.cpp`
* set paramter `useArm` to `both` in `robotic/botop/src/BotOp/bot.cpp` 

## Test Code

* test code, no conda environment!
  ```
  import robotic as ry
  import numpy as np
  import time
  print('version:', ry.__version__, ry.compiled())
  
  C = ry.Config()
  
  # C.addFile(ry.raiPath('panda/panda.g'))
  # C.view(True)
  
  C = ry.Config()
  C.addFile(ry.raiPath('scenarios/pandaSingle.g'))
  pcl = C.addFrame('pcl', 'cameraWrist')
  C.view(False, 'this is your workspace data structure C -- NOT THE SIMULTATION')
  
  # True = real robot!!
  bot = ry.BotOp(C, useRealRobot=True)
  
  
  # first motion
  # q = bot.get_qHome()
  # q[1] = q[1] + .05
  
  # bot.moveTo(q)
  # bot.wait(C)
  # print('first motion done')
  
  # bot.moveTo(bot.get_qHome())
  # bot.wait(C)
  
  # realsense
  # pcl = C.getFrame("pcl")
  # pcl.setShape(ry.ST.pointCloud, [2]) # the size here is pixel size for display
  # bot.sync(C)
  
  # count = 0
  
  # while bot.getKeyPressed()!=ord('q'):
  #     image, depth, points = bot.getImageDepthPcl("cameraWrist")
  #     pcl.setPointCloud(points, image)
  #     pcl.setColor([1,0,0])
  #     bot.sync(C, .1)
  
  #     if bot.getTimeToEnd()<=0.:
  #         bot.moveTo(q)
  #         bot.moveTo(bot.get_qHome())
  #         count = count + 1
  #     if count>=3:
  #         break
  
  # #slow close
  # bot.gripperMove(ry._left, width=.0, speed=.1)
  
  # while not bot.gripperDone(ry._left):
  #     bot.sync(C)
  
  # #fast open
  # bot.gripperMove(ry._left, width=.08, speed=1.)
  
  # while not bot.gripperDone(ry._left):
  #     bot.sync(C)
  
  # C.view(True, 'floating=False, damping=True -- Try moving the robot by hand!\n-- press any key to continue --')
  
  # C.view(True)
  
  # can freely move
  # bot.hold(floating=True, damping=False)
  # C.view(True, 'floating=True, damping=False -- Try moving the robot by hand!\n-- press any key to continue --')
  
  # # cannot freely move
  # bot.hold(floating=True, damping=True)
  # C.view(True, 'floating=True, damping=True -- Try moving the robot by hand!\n-- press any key to continue --')
  
  
  # # kinesthetic teaching
  # while bot.getKeyPressed()!=ord('q'):
  #     bot.hold(floating=True, damping=False)
  #     C.view(False, 'floating=True, damping=False -- Try moving the robot by hand!\n-- press any key to continue --')
  #     print("joint", C.getJointState())
  #     bot.sync(C, .1)
  
  # pick pos 0.70823282  0.5145498  -0.50892331 -2.43935441  0.69740008  2.8310342 0.28498277
  # pre-place 0.48103646  0.71926825 -0.93559304 -1.25053177  0.54012957  1.68139181 0.23365277
  # place 0.48103646  0.71926825 -0.93559304 -1.25053177  0.54012957  1.68139181 0.23365277
  
  q = bot.get_qHome()
  # print("home ", q) # [ 0.  -0.5  0.  -2.   0.   2.  -0.5]
  # q[1] = q[1] + .05
  # .08
  bot.gripperMove(ry._left, width=.08, speed=.1)
  bot.wait(C)
  
  bot.moveTo(q)
  bot.wait(C)
  
  pick_pos = [0.70823282,  0.5145498,  -0.50892331, -2.43935441,  0.69740008,  2.8310342, 0.28498277]
  bot.moveTo(pick_pos)
  bot.wait(C)
  bot.gripperMove(ry._left, width=.0, speed=.2)
  # bot.wait(C)
  time.sleep(1)
  
  # pre_place = [0.48103646, 0.71926825, -0.93559304, -1.25053177, 0.54012957, 1.68139181, 0.23365277]
  # bot.moveTo(pre_place)
  # bot.wait(C)
  
  # place = [0.48103646, 0.71926825, -0.93559304, -1.25053177, 0.54012957, 1.68139181, 0.23365277]
  place = [0.45018898, 1.05914621, -0.86702589, -1.228143, 0.75709283, 1.97062684, 0.20938338]
  bot.moveTo(place)
  bot.wait(C)
  time.sleep(0.7)
  bot.gripperMove(ry._left, width=.08, speed=.1)
  ```
* komo_bimanual.py
  ```
  import robotic as ry
  import numpy as np
  import time
  print('version:', ry.__version__, ry.compiled())
  
  C = ry.Config()
  
  # C.addFile(ry.raiPath('panda/panda.g'))
  # C.view(True)
  
  C = ry.Config()
  C.addFile(ry.raiPath('scenarios/pandaDual.g'))
  pcl = C.addFrame('pcl', 'cameraWrist')
  
  C.addFrame('tube') \
      .setPosition([0.,.1, .9]) \
      .setShape(ry.ST.ssBox, size=[.9,.06,.06,.005]) \
      .setColor([1,.5,0]) \
      .setContact(1)
  
  C.addFrame('goal') \
      .setPosition([0.,-.1, 1.1]) \
      .setQuaternion([.1, 0, 0, .0]) \
      .setShape(ry.ST.ssBox, size=[.9,.06,.06,.005]) \
      .setColor([1,.7,0]) \
      .setContact(1)
  
  C.addFrame('goal2') \
      .setPosition([0.,.3, 1.3]) \
      .setQuaternion([.1, 0, 0, .0]) \
      .setShape(ry.ST.ssBox, size=[.9,.06,.06,.005]) \
      .setColor([1,.7,0]) \
      .setContact(1)
  
  
  C.view(True, 'this is your workspace data structure C -- NOT THE SIMULTATION')
  
  # True = real robot!!
  bot = ry.BotOp(C, useRealRobot=True)
  
  bot.sync(C)
  bot.moveTo(bot.get_qHome())
  bot.wait(C)
  l_gripper = C.getFrame("l_gripper")
  r_gripper = C.getFrame("r_gripper")
  tube = C.getFrame("tube")
  l= tube.getSize()[0]
  print("l ", l)
  # print(C.getJointState())
  
  # ###### komo ###############
  komo = ry.KOMO(C, phases=1, slicesPerPhase=1, kOrder=1, enableCollisions=False)
  komo.addControlObjective([], 0, 1e-1)
  komo.addControlObjective([], 1, 1e0)
  komo.addObjective([1], ry.FS.positionRel, ['l_gripper', 'tube'], ry.OT.eq, [1e1], target=[-l/2,0,0])
  komo.addObjective([1], ry.FS.positionRel, ['r_gripper', 'tube'], ry.OT.eq, [1e1], target=[l/2,0,0])
  komo.addObjective([1], ry.FS.scalarProductXX, ['l_gripper', 'tube'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXZ, ['l_gripper', 'tube'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductYZ, ['l_gripper', 'tube'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXX, ['r_gripper', 'tube'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXZ, ['r_gripper', 'tube'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductYZ, ['r_gripper', 'tube'], ry.OT.eq, [1e1], [0])
  ret = ry.NLP_Solver(komo.nlp(), verbose=0) .solve()
  
  q = komo.getPath()
  print('size of path:', q.shape)
  # print("q-1", q[-1])
  q0 = q[-1]
  # bot.moveTo(q[-1])
  # bot.wait(C)
  # print("l-r ",l_gripper.getPosition()-r_gripper.getPosition())
  
  komo = ry.KOMO(C, phases=1, slicesPerPhase=1, kOrder=1, enableCollisions=False)
  komo.addControlObjective([], 0, 1e-1)
  komo.addControlObjective([], 1, 1e0)
  komo.addObjective([1], ry.FS.positionRel, ['l_gripper', 'goal'], ry.OT.eq, [1e1], target=[-l/2,0,0])
  komo.addObjective([1], ry.FS.positionRel, ['r_gripper', 'goal'], ry.OT.eq, [1e1], target=[l/2,0,0])
  komo.addObjective([1], ry.FS.scalarProductXX, ['l_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXZ, ['l_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductYZ, ['l_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXX, ['r_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXZ, ['r_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductYZ, ['r_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  ret = ry.NLP_Solver(komo.nlp(), verbose=0) .solve()
  q = komo.getPath()
  q1 = q[-1]
  
  # bot.moveTo(q0)
  # bot.wait(C)
  # bot.moveTo(q1)
  # bot.wait(C)
  
  komo = ry.KOMO(C, phases=1, slicesPerPhase=20, kOrder=1, enableCollisions=False)
  komo.addControlObjective([], 0, 1e-1)
  komo.addControlObjective([], 1, 1e0)
  komo.addObjective([0.3], ry.FS.jointState, [], ry.OT.sos, [1e1], target=q0)
  komo.addObjective([0.3, 1], ry.FS.positionDiff, ['l_gripper', 'r_gripper'], ry.OT.eq, [1e1], target=[-l,0,0])
  # komo.addObjective([0, 1], ry.FS.quaternionDiff, ['l_gripper', 'r_gripper'], ry.OT.eq, [1e1], target=[0,0,0,0])
  komo.addObjective([0.7], ry.FS.positionRel, ['l_gripper', 'goal'], ry.OT.eq, [1e1], target=[-l/2,0,0])
  komo.addObjective([0.7], ry.FS.positionRel, ['r_gripper', 'goal'], ry.OT.eq, [1e1], target=[l/2,0,0])
  komo.addObjective([0.7], ry.FS.scalarProductXX, ['l_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([0.7], ry.FS.scalarProductXZ, ['l_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([0.7], ry.FS.scalarProductYZ, ['l_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([0.7], ry.FS.scalarProductXX, ['r_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([0.7], ry.FS.scalarProductXZ, ['r_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([0.7], ry.FS.scalarProductYZ, ['r_gripper', 'goal'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.positionRel, ['l_gripper', 'goal2'], ry.OT.eq, [1e1], target=[-l/2,0,0])
  komo.addObjective([1], ry.FS.positionRel, ['r_gripper', 'goal2'], ry.OT.eq, [1e1], target=[l/2,0,0])
  komo.addObjective([1], ry.FS.scalarProductXX, ['l_gripper', 'goal2'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXZ, ['l_gripper', 'goal2'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductYZ, ['l_gripper', 'goal2'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXX, ['r_gripper', 'goal2'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductXZ, ['r_gripper', 'goal2'], ry.OT.eq, [1e1], [0])
  komo.addObjective([1], ry.FS.scalarProductYZ, ['r_gripper', 'goal2'], ry.OT.eq, [1e1], [0])
  
  # positionRel is not working very well
  
  # komo = ry.KOMO(C, phases=1, slicesPerPhase=10, kOrder=1, enableCollisions=False)
  # komo.addControlObjective([], 0, 1e-1)
  # komo.addControlObjective([], 1, 1e0)
  # komo.addObjective([0.3], ry.FS.jointState, [], ry.OT.sos, [1e1], target=q0)
  # komo.addObjective([0.3, 1], ry.FS.positionDiff, ['l_gripper', 'r_gripper'], ry.OT.eq, [1e1], target=[-l,0,0])
  # # komo.addObjective([0, 1], ry.FS.quaternionDiff, ['l_gripper', 'r_gripper'], ry.OT.eq, [1e1], target=[0,0,0,0])
  # komo.addObjective([1], ry.FS.jointState, [], ry.OT.sos, [1e1], target=q1)
  
  ret = ry.NLP_Solver(komo.nlp(), verbose=0) .solve()
  q = komo.getPath()
  
  # print("q0, ", q0)
  # print("cal ", q[0])
  #
  # for t in range(q.shape[0]):
  #     bot.moveTo(q[t])
  #     bot.wait(C)
  
  #     print("l-r ",l_gripper.getPosition()-r_gripper.getPosition())
  #     # print("r ",r_gripper.getPosition())
  #     # print( r_gripper.getQuaternion())
  
  # be careful about the max velocity!!!
  bot.moveAutoTimed(q, .5, .2) # path, max vel, max acc
  while bot.getTimeToEnd()>0:
      bot.sync(C, .1)
  ```
