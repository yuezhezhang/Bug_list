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
16. [merge gifs using imageio](https://stackoverflow.com/questions/73431547/how-do-i-connect-two-gifs-to-play-one-after-another-in-python)
    ```
    import imageio.v3 as iio
    import numpy as np

    # assume same FPS
    frames = np.vstack([
        iio.imread("my_first.gif"),
        iio.imread("my_second.gif"),
    ])
    
    # get duration each frame is displayed
    duration = iio.immeta("my_first.gif")["duration"]
    
    iio.imwrite("combined.gif", frames, duration=duration)
    ```
17. [images to gif using imageio](https://stackoverflow.com/questions/41228209/making-gif-from-images-using-imageio-in-python?__cf_chl_tk=q0BQAsfZzhcKkJDSppuojedkZ9ucjIJk9jtdA9uW3LE-1770127071-1.0.1.1-O24t37dmX83Bwf4dpoWwxBZUWp88o2jo_Ki7jF2DeMw)
    ```
    import os
    import imageio
    
    png_dir = '../animation/png'
    images = []
    for file_name in sorted(os.listdir(png_dir)):
        if file_name.endswith('.png'):
            file_path = os.path.join(png_dir, file_name)
            images.append(imageio.imread(file_path))
    
    # Make it pause at the end so that the viewers can ponder
    for _ in range(10):
        images.append(imageio.imread(file_path))
    
    # imageio.mimsave('../animation/gif/movie.gif', images, fps=55)
    iio.imwrite("../animation/gif/movie.gif", images, duration=0.1)
    ```
