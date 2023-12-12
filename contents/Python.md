## Python
1. [Import module from another folder](https://stackoverflow.com/questions/58084072/python-module-not-found-but-exists-in-folder/58084390#58084390)
* If I have a folder like
   ```
      .
   └── my_project
       ├── first_folder
       ├── second_folder
       └── third_folder
   ```
 * We can do one of the followings:
 * `cd ~/my_project && export PYTHONPATH=$(pwd)`
 * `cd ~/my_project && export PATH=$PATH:$(pwd)`
 
 2. Update pytorch version in rlgpu env
 * run `conda update pytorch torchvision` within rlgpu env
 ```
  environment location: /home/zyz/anaconda3/envs/rlgpu

  added / updated specs:
    - pytorch
    - torchvision   
 ```
 * to 1.10.2, but not compatible with cuda
 3. show the version of pytorch
 ```
 import torch
 torch.__version__
 ```
 4. show the version of cudatoolkit
 ```
 conda list cudatoolkit
 ``` 
 5. run `conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch`
 6. [conda commands cheat sheet](https://hcc.unl.edu/docs/attachments/11635089.pdf)
 7. [Guide to python command line argumens](https://levelup.gitconnected.com/the-easy-guide-to-python-command-line-arguments-96b4607baea1), [argparse tutorial](https://docs.python.org/3/library/argparse.html#creating-a-parser)
 
### Importing python file as module

#### 1. Import a file in the same directory
* **Given that**
  ```
  examples
  ├── main.py
  ├── source1.py
  ```
* In the `main.py` file, write:
  ```
  import source1
  
  source1.func()
  ```
#### 2. Import a file in a subdirectory
* **Given that**
  ```
  examples
  ├── subdir
  │   ├── __init__.py
  │   └── source2.py
  ├── main.py
  ```
* In the `main.py` file, write:
  ```
  from subdir import source2

  source2.print_f()
  ```
  **Or**
  ```
  import subdir.source2 as m

  m.print_f()
  ```
#### 3. Import a file in a different directory
* **Given that**
  ```
  examples
  └── main.py
  params
  ├── __init__.py
  └── source3.py
  ```
* In the `main.py` file, write:
  ```
  import sys
  sys.path.append('../')
  from params import source3

  source3.print_f()
  ```
* **Or**
  ```
  import sys
  sys.path.append('../')
  import params.source3 as source3

  source3.print_f()
  ```
* **Given that**
  ```
  examples
  └── main.py
  params
  ├── subdir.py
  │   ├── __init__.py
  │   └── source4.py
  ```
* In the `main.py` file, write:
  ```
  import sys
  sys.path.append('../')
  import params.subdir.source4 as source4

  source4.print_f()
  ```
#### Some references
* [Overall guidance](https://csatlas.com/python-import-file-module/#import_a_file_in_the_same_directory)
* [Suggestion to adding to python path](https://stackoverflow.com/questions/4383571/importing-files-from-different-folder?page=1&tab=scoredesc#tab-top)
* [Suggestion to installing packages](https://stackoverflow.com/questions/43476403/importerror-no-module-named-something)

### If-else
* Bug
  ```
  a = 1
  if a == 0 or 2:
     print('hhh') # will always print this
  else:
     print('heyyy')
  ```
* Correct
  ```
  a = 1
  if a == 0 or a == 2:
     print('hhh')
  else:
     print('heyyy') # here
  ```
  
### Matplotlib
* [PLot a circle](https://stackoverflow.com/questions/9215658/plot-a-circle-with-pyplot)
* [Issue of plotting circle as oval](https://stackoverflow.com/questions/9230389/why-is-matplotlib-plotting-my-circles-as-ovals)
* [List of colors](https://matplotlib.org/stable/gallery/color/named_colors.html)
* 

## Pytorch
* [torch.index_select](https://pytorch.org/docs/stable/generated/torch.index_select.html)
* [torch.squeeze](https://pytorch.org/docs/stable/generated/torch.squeeze.html)
* [torch.diagonal](https://pytorch.org/docs/stable/generated/torch.diagonal.html)
* [torch.fliplr](https://pytorch.org/docs/stable/generated/torch.fliplr.html)
* [torch.topk](https://pytorch.org/docs/stable/generated/torch.topk.html)


### Python-Ros
* [Install rospkg](https://answers.ros.org/question/356188/importerror-no-module-named-rospkg/)
   * `File "/opt/ros/noetic/lib/python3/dist-packages/roslib/launcher.py", line 42, in <module> import rospkg ModuleNotFoundError: No module named 'rospkg'`
   * Run `sudo pip install --target=/opt/ros/noetic/lib/python3/dist-packages rospkg`

### Regular Expression
* See [docs](https://docs.python.org/zh-cn/3/library/re.html#regular-expression-objects) and [this](https://www.runoob.com/python/python-reg-expressions.html)
* To check a character within range：
  ```
  if re.search(r'[0-9A-Fa-f]', x):
     pass
  ``` 
