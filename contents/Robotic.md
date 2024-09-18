1. Install Robotic from source
  * [see](https://github.com/MarcToussaint/robotic/tree/master)
  * Change path in `install.sh` from `git=${HOME}/git` to `git=${HOME}/git/marc`
  * Issue of `Could NOT find Freetype (missing: FREETYPE_LIBRARY FREETYPE_INCLUDE_DIRS)`
      * `sudo apt-get install libfreetype6-dev` could solve, [see](https://github.com/tpaviot/oce/issues/720)
