# webots2023b_ros2_docker
### Dowload the docker
```bash
docker pull registry.cn-guangzhou.aliyuncs.com/ddt_robot/ubuntu:webot2023b-v1
```

### A refer to start the docker

```bash
sudo docker run -v path/above/your/project:/mnt/dev -w /mnt/dev --rm  --gpus all --net=host --privileged -e DISPLAY=$DISPLAY -e QT_X11_NO_MITSHM=1  -e CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda -it registry.cn-guangzhou.aliyuncs.com/ddt_robot/ubuntu:webot2023b-v1

# For example: Dowloads is the directory above the project tita_rl_sim2sim2real
sudo docker run -v ~/Downloads:/mnt/dev -w /mnt/dev --rm  --gpus all --net=host --privileged -e DISPLAY=$DISPLAY -e QT_X11_NO_MITSHM=1  -e CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda -it registry.cn-guangzhou.aliyuncs.com/ddt_robot/ubuntu:webot2023b-v1


```



### Try starting the webots，and shall see the webots GUI:

```bash
webots
```

### Check ros2 :

```bash
source /opt/ros/humble/setup.bash

ros2 topic list

```

### In the host, clone this project, and copy the webots_ros2 file under your project:

```bash

git clone git@github.com:DDTRobot/webots2023b_ros2_docker.git

cp -r webots_ros2 path/to/your/project

```

### In docker, get into webots_ros2, and compile webots_ros2

```bash

./start_docker #start the docker

cd webots_ros2

colcon build

source install/setup.bash

```

### Now, you can go to your project file, and compile your project, for example :

```bash

#In /mnt/dev :

cd tita_rl_sim2sim2real

source /opt/ros/humble/setup.bash && colcon build --packages-up-to locomotion_bringup webots_bridge robot_inertia_calculator template_ros2_controller tita_controller joy_controller keyboard_controller

```

### If you any package is missing (e.g. pinocchio), try :

```bash

apt update

apt install ros-humble-pinocchio

#Then delete the build file and build again

```

### If you meet "xcb" error :

```bash

#Add the following in your ~/.bashrc:

xhost +

```

### Plaese use tensorrt and compile in the docker, rather than the host!! For example:

```bash

#In docker : /mnt/dev, convert the onnx to .engine:

/usr/src/tensorrt/bin/trtexec --onnx=your_onnx.onnx --saveEngine=your_engine.engine

```

### Remember to change your engine file path under the path of docker, e.g. :

```bash

# /mnt/dev is the path in your docker, not int the host
cuda_test_ = std::make_shared<CudaTest>("/mnt/dev/model_gn.engine");

```

