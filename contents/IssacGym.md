## Issac Gym
1. Find isaac gym here https://developer.nvidia.com/isaac-gym. Register and download the simulator.  Within the download, there is a folder called 'docs'. Follow the instructions

2. Install in a new conda environment (In the root directory)
```
./create_conda_env_rlgpu.sh
```
3. Activate by running
```
conda activate rlgpu
```
4. Deactivate by running
```
conda deactivate
```
5. Install Example RL Environments
Visit https://github.com/NVIDIA-Omniverse/IsaacGymEnvs and follow the setup instructions in the README.

6. Trouble shooting
* Error `ImportError: libpython3.7m.so.1.0: cannot open shared object file: No such file or directory`
* Set the LD_LIBRARY_PATH variable in rlgpu environment (should be updated every time) 
   ```
   export LD_LIBRARY_PATH=/home/zyz/anaconda3/envs/rlgpu/lib
   ```
* Then run the simple example would be fine.
* We can `echo $PATH` in different conda environment

## Gym_envs_urdf
1. Rotate the view of camera: alt + mouse
