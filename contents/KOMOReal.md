## Installation

* install physx error, fix this by [see](https://stackoverflow.com/questions/26380407/cmake-clang-is-not-able-compile-a-simple-test-program-fedora-20)
  ```
  sudo apt install libstdc++-12-dev
  ```
* can not find glm headers, [see](https://stackoverflow.com/questions/28977455/why-cant-c-find-glm-headers)
  ```
  sudo apt-get install libglm-dev
  ``` 
* current robotic version 1.3 and update its submodule
  ```
  git reset --hard a9adb1b50cca67e614f88481371bb7d76ba0c25a
  git submodule update --recursive
  ```
  for display current commit version
  ```
  git rev-parse HEAD
  ```
* update franka ip `192.168.2.55` in `robotic/botop/src/Franka/franka.cpp` and `FrankaGripper.cpp`
* compile
  ```
  cd robotic
  make -C build _robotic install

  export PATH="$HOME/.local/bin:$PATH"
  ry-bot -real -up -home
  ```
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