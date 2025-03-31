## ZED 2

### Installation
1. Install CUDA in `Downloads/cuda11_and_zed`, [11.8, runfile, select no driver](https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local)

   In ~/.bashrc
   ```
   export PATH=$PATH:/usr/local/cuda-11.8/bin
   export LD_LIBRARY_PATH=$PATH:/usr/local/cuda-11.8/lib64
   ```
2. Install [zed SDK](https://www.stereolabs.com/docs/installation/linux)

### Running
1. Multiple cameras (not easy to connect)
   ```
   roscore

   roslaunch zed_wrapper rviz_dual.launch

   # plug in zed_head cameara
   roslaunch zed_wrapper zed2i_head.launch serial_number:=39164257

   # change `zed_head_map` and `zed_head_odom` to `zed_chest_map` and `zed_chest_odom` in `common.yaml`, and then plug in zed_chest camera
   roslaunch zed_wrapper zed2i_chest.launch serial_number:=33124271
   ```
2. Use rosbag to save topics
   ```
   rosbag record /tf /tf_static /zed_chest/joint_states /zed_chest/zed2i_chest_node/confidence/confidence_map /zed_chest/zed2i_chest_node/depth/camera_info /zed_chest/zed2i_chest_node/depth/depth_registered /zed_chest/zed2i_chest_node/disparity/disparity_image /zed_chest/zed2i_chest_node/imu/data /zed_chest/zed2i_chest_node/imu/data_raw /zed_chest/zed2i_chest_node/imu/mag /zed_chest/zed2i_chest_node/left/camera_info /zed_chest/zed2i_chest_node/left/image_rect_color /zed_chest/zed2i_chest_node/left_cam_imu_transform /zed_chest/zed2i_chest_node/odom /zed_chest/zed2i_chest_node/odom/status /zed_chest/zed2i_chest_node/path_map /zed_chest/zed2i_chest_node/path_odom /zed_chest/zed2i_chest_node/plane /zed_chest/zed2i_chest_node/plane_marker /zed_chest/zed2i_chest_node/pose /zed_chest/zed2i_chest_node/pose/status /zed_chest/zed2i_chest_node/pose_with_covariance /zed_chest/zed2i_chest_node/right/camera_info /zed_chest/zed2i_chest_node/right/image_rect_color /zed_head/joint_states /zed_head/zed2i_head_node/confidence/confidence_map /zed_head/zed2i_head_node/depth/camera_info /zed_head/zed2i_head_node/depth/depth_registered /zed_head/zed2i_head_node/disparity/disparity_image /zed_head/zed2i_head_node/imu/data /zed_head/zed2i_head_node/imu/data_raw /zed_head/zed2i_head_node/imu/mag /zed_head/zed2i_head_node/left/camera_info /zed_head/zed2i_head_node/left/image_rect_color /zed_head/zed2i_head_node/left_cam_imu_transform /zed_head/zed2i_head_node/odom /zed_head/zed2i_head_node/odom/status /zed_head/zed2i_head_node/path_map /zed_head/zed2i_head_node/path_odom /zed_head/zed2i_head_node/plane /zed_head/zed2i_head_node/plane_marker /zed_head/zed2i_head_node/pose /zed_head/zed2i_head_node/pose/status /zed_head/zed2i_head_node/pose_with_covariance /zed_head/zed2i_head_node/right/camera_info /zed_head/zed2i_head_node/right/image_rect_color 
   ```

3. Vscode convert multiple lines to one line, hit `Ctrl + Shift + P` or in `preferences/keyboard shortcuts` search `joinLines`, I add the shortcut to be `Ctrl + J + K`
