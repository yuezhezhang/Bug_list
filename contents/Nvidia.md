## Cuda
* [Install cuda 11.8 on ubuntu 20 with driver 535](https://www.enablegeek.com/blog/setting-up-cuda-and-cudnn-on-ubuntu-20-04/)
  ```
  wget  https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
  sudo sh cuda_11.8.0_520.61.05_linux.run --toolkit --silent --override
  ```
* [Removing Nvidia CUDA Toolkit](https://askubuntu.com/questions/530043/removing-nvidia-cuda-toolkit-and-installing-new-one)
  ```
  sudo apt-get remove --auto-remove nvidia-cuda-toolkit
  ```
* [Difference between nvcc --version and nvidia-smi](https://stackoverflow.com/questions/53422407/different-cuda-versions-shown-by-nvcc-and-nvidia-smi)
    * `nvidia-smi`: The nvidia-smi tool gets installed by the GPU driver installer, and generally has the GPU driver in view, not anything installed by the CUDA toolkit installer. **This has no connection to the installed CUDA runtime version.**
    * `nvcc --version`: the CUDA compiler-driver tool that is installed with the CUDA toolkit, **will always report the CUDA runtime version** that it was built to recognize. It doesn't know anything about what driver version is installed, or even if a GPU driver is installed.
    * Therefore, by design, these two numbers don't necessarily match, as they are reflective of two different things.
