1. Install Robotic from source
  * [see](https://github.com/MarcToussaint/robotic/tree/master)
  * Change path in `install.sh` from `git=${HOME}/git` to `git=${HOME}/git/marc`
  * Issue of `Could NOT find Freetype (missing: FREETYPE_LIBRARY FREETYPE_INCLUDE_DIRS)`
      * `sudo apt-get install libfreetype6-dev` could solve, [see](https://github.com/tpaviot/oce/issues/720)
  * Issue of `fatal error: glm/glm.hpp: No such file or director`
      * `sudo apt-get install libglm-dev` could solve, [see](https://stackoverflow.com/questions/28977455/why-cant-c-find-glm-headers)
  * I tried to install everything from conda env 
  * Everything is installed in `.local/lib/python*/site-packages/robotic`, sth weird 
