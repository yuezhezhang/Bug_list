1. Install Robotic from source
  * [see](https://github.com/MarcToussaint/robotic/tree/master)
  * Change path in `install.sh` from `git=${HOME}/git` to `git=${HOME}/git/marc`
  * Issue of `Could NOT find Freetype (missing: FREETYPE_LIBRARY FREETYPE_INCLUDE_DIRS)`
      * `sudo apt-get install libfreetype6-dev` could solve, [see](https://github.com/tpaviot/oce/issues/720)
  * Issue of `fatal error: glm/glm.hpp: No such file or director`
      * `sudo apt-get install libglm-dev` could solve, [see](https://stackoverflow.com/questions/28977455/why-cant-c-find-glm-headers)
  * I tried to install everything from conda env 
  * Everything is installed in `.local/lib/python*/site-packages/robotic`, sth weird 

2. Install [pyroboplan](https://github.com/sea-bass/pyroboplan)
   ```
   conda create -n pyroboplan python=3.10
   conda activate pyroboplan
   conda install pinocchio -c conda-forge
   git clone https://github.com/sea-bass/pyroboplan.git
   cd pyroboplan && pip install -e. 
   ```
   an issue has been solved, [see](https://github.com/stack-of-tasks/pinocchio/issues/1960#issuecomment-2272676580)
   `pip install pyroboplan` is not working
3. simple bullet panda grasping, [video](https://www.youtube.com/watch?v=yKShjSTayco), [code](https://github.com/bulletphysics/bullet3/blob/master/examples/pybullet/gym/pybullet_robots/panda/loadpanda_grasp.py) 
