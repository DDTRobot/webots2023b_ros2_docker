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
