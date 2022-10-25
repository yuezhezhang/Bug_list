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
