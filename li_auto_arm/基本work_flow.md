# 加载docker
docker load -i ###.tar

# 运行docker（cd 到工作空间）
bash run_docker.sh  #/A_project/IRC_LI_auto_ws/irc_charging_robot_li_auto/docker/imo/x64
docker run --rm --privileged=true -it --network=host --name u22_04_humble  --shm-size=4g -v /home/$USER:/home/$USER -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY 5be037528a48 /bin/bash
docker run --rm --privileged=true -it --network=host --name u22_04_humble --gpus all --shm-size=4g -v /home/$USER:/home/$USER -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY 9f5147edb3a2 /bin/bash

# 在其他终端进入同一docker
docker ps -a  # 查看container
docker exec -it 3f74c2bb1774 bash #进入对应的 container ID

# 编译控制相关节点
colcon build --packages-select artiarm_bringup
colcon build --packages-select artiarm_hardware
colcon build --packages-select robot_global_interfaces robot_perception_camera_hand_py robot_camera_driver artiarm_bringup artiarm_hardware  charger_config charger_description comm_interface robot_commu 

# 启动相关节点的launch 文件
source install/setup.bash
ros2 launch artiarm_bringup robot_hardware_rviz.launch.py

# 运行控制图形化界面
source install/setup.bash
ros2 run artiarm_bringup trajectory_gui.py
# 1. 安装 Xvfb（若未安装）
sudo apt install -y xvfb

# 2. 启动虚拟 X11 服务（:0 对应 unix:0），后台运行
Xvfb :0 -screen 0 1920x1080x24 -ac &

# 3. 导出主机 DISPLAY 变量
export DISPLAY=:0

# 4. 开放 X11 权限
xhost +local:

# 5. 重新启动/进入容器
bash run_docker.sh  # 或重新执行步骤2的启动命令
Conda 空间（只在当前终端有效）
conda create -n irc_li_auto python=3.10 -y # 创建了 名为 irc_li_auto 的conda 空间，Python 版本为 3.10
conda activate irc_li_auto  # 激活 irc_li_auto 空间
conda deactivate    # 关闭 irc_li_auto 空间

# CAN  设置
pip install python-can

sudo ip link set can0 type can bitrate 1000000 # 设置发送队列长度
sudo ip link set can0 txqueuelen 1000
sudo ip link set can0 up
sudo ip link show
sudo candump can0

# 待办
[x] clcon packages-select 选项的安装，注意是否区分conda 空间
[x] docker 跑不起来 gpu 的原因，缺一个nvidia-container-toolkit


colcon build --packages-skip rslidar_sdk  OpenCLHeadersCpp image_pipeline_demo_cpp

编译moveit2
colcon build --mixin release --parallel-workers 1

