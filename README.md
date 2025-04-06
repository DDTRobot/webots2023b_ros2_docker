# webots2023b_ros2_docker
### Dowload the docker
```bash
docker pull registry.cn-guangzhou.aliyuncs.com/ddt_robot/ubuntu:webot2023b-v1
```

### A refer to start the docker

```bash
sudo docker run -v path/to/your/project:/mnt/dev -w /mnt/dev --rm  --gpus all --net=host --privileged -e DISPLAY=$DISPLAY -e QT_X11_NO_MITSHM=1  -e CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda -it ubuntu:webot2023b-v1
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

./start_docker

cd webots_ros

colcon build

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

```
