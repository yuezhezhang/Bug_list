## Useful tools
1. [Online latex table creater](https://www.tablesgenerator.com/)
2. [Online video to gif converter](https://ezgif.com/video-to-gif)
3. [Screenshot with fixed size -- shutter](https://askubuntu.com/questions/262253/how-do-i-take-a-screenshot-with-dimensions)
   * [To install shutter on ubuntu 20.04](https://www.tecmint.com/install-shutter-in-ubuntu/)
4. [Record screen -- kazam](https://itsfoss.com/kazam-screen-recorder/)
5. [CheatSheets](https://cheatsheets.zip/)
6. Vim
   * [vim cheatsheet](https://cheatsheets.zip/vim)
   * neovim, [website](https://neovim.io/), [github](https://github.com/neovim/neovim)
7. Zotero
   * [Identifying Collections an Item is](https://www.zotero.org/support/collections_and_tags): Select the item, press the key Alt 
8. [Freeconvert](https://www.freeconvert.com/)
   * [mov to mp4](https://www.freeconvert.com/mov-to-mp4/)
   * [video compress](https://www.freeconvert.com/video-compressor/)
9. [Creatly](https://app.creately.com/d/start/dashboard)
   * draw ppt diagram
10. [Online mesh creator](https://app.meshinspector.com/RMI/)
11. [Video compressor](https://www.freeconvert.com/video-compressor)
12. Adobe, needs account
    * Adobe Premiere, video editing, speed up, blur
    * Adobe Illustrator, draw diagram
    * Adobe Express, put some images together
13. pngs to mp4 (quality is ok)
    * `ffmpeg -framerate 30 -i frame_%04d.png -c:v libx264 -crf 18 -pix_fmt yuv420p output.mp4`, check [this](https://stackoverflow.com/questions/24961127/how-to-create-a-video-from-images-with-ffmpeg)
14. pngs to high quality gif
    * `gifski -r 12.5 -o videoname.gif pngname*.png`
    * but now get "ImportError: libcblas.so.3: cannot open shared object file: No such file or directory", not working using [this](https://stackoverflow.com/questions/53347759/importerror-libcblas-so-3-cannot-open-shared-object-file-no-such-file-or-dire/54954503) and [that](https://stackoverflow.com/questions/75414336/libblas-so-3-cannot-open-shared-object-file-no-such-file-or-directory-but-it)
15. video to png
    * `ffmpeg -i video.mp4 frame%04d.png`
