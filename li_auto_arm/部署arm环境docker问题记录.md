# arm 环境中docker artiarm_bringup 编译问题解决

## 清理之前的编译缓存（关键）
colcon build --packages-select artiarm_bringup --cmake-clean-cache

## 强制指定系统OpenSSL和Python库路径
colcon build --packages-select artiarm_bringup \
  --cmake-args \
  -DCMAKE_LIBRARY_PATH=/usr/lib/aarch64-linux-gnu \
  -DCMAKE_INCLUDE_PATH=/usr/include \
  -DCMAKE_EXE_LINKER_FLAGS="-L/usr/lib/aarch64-linux-gnu -Wl,-rpath=/usr/lib/aarch64-linux-gnu"


# 永久修复方法（没有尝试）修改CMakeLists.txt文件
## 强制指定系统库路径，覆盖conda的库
set(CMAKE_LIBRARY_PATH "/usr/lib/aarch64-linux-gnu" ${CMAKE_LIBRARY_PATH})
set(CMAKE_INCLUDE_PATH "/usr/include" ${CMAKE_INCLUDE_PATH})

## 强制链接器使用系统库，并设置运行时库路径
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -L/usr/lib/aarch64-linux-gnu -Wl,-rpath=/usr/lib/aarch64-linux-gnu")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -L/usr/lib/aarch64-linux-gnu -Wl,-rpath=/usr/lib/aarch64-linux-gnu")

## 显式指定使用系统的OpenSSL库
find_package(OpenSSL REQUIRED)
link_directories(/usr/lib/aarch64-linux-gnu)
include_directories(${OPENSSL_INCLUDE_DIR})

如果你有add_executable(joints_plan ...)，需要显式链接系统库
找到对应的target_link_libraries，添加以下内容：
target_link_libraries(joints_plan
  ${OPENSSL_LIBRARIES}
  /usr/lib/aarch64-linux-gnu/libssl.so.3
  /usr/lib/aarch64-linux-gnu/libcrypto.so.3
  /usr/lib/aarch64-linux-gnu/libpython3.10.so.1.0
)

# 修改docker数据目录
## 1. 查看当前docker数据目录
  sudo docker info | grep "Docker Root Dir"

## 2. 创建新的docker数据目录
  sudo mkdir xxx/docker

## 3. 修改docker配置文件
  mkdir -p /etc/systemd/system/docker.service.d/
  vi /etc/systemd/system/docker.service.d/devicemapper.conf
### 添加以下内容
  [Service]
  ExecStart=
  ExecStart=/usr/bin/dockerd  --data-root=xxx/docker

## 4.设置正确的属主和权限（Docker 进程以 root 运行，需确保权限足够）
  sudo chown root:root xxx/docker
  sudo chmod 700 xxx/docker
## 5.重启docker服务
### 重新加载 systemd 配置
  sudo systemctl daemon-reload
### 重启 Docker 服务
  sudo systemctl restart docker
### 验证 Docker 是否正常运行
  sudo systemctl status docker

# docker 网络配置
## 1. 将 iptables 切换到 legacy 模式
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy

## 2. 确认切换成功（输出应显示 "legacy"）
update-alternatives --list iptables

## 3. 重新启动 Docker 服务
sudo systemctl restart docker

## 4. 检查 Docker 服务状态
sudo systemctl status docker

## 5. 验证 iptables 工作模式
sudo update-alternatives --query iptables

# 切换docker存储驱动
## 1. 停止 Docker 服务
sudo systemctl stop docker
sudo systemctl stop docker.socket

## 2. 备份原有 Docker 配置（如有）
sudo cp /etc/docker/daemon.json /etc/docker/daemon.json.bak 2>/dev/null || true

## 3. 配置 vfs 存储驱动
sudo tee /etc/docker/daemon.json <<EOF
{
  "storage-driver": "vfs"
}
EOF

## 4. 清理旧存储驱动残留（可选，避免冲突）
sudo rm -rf /var/lib/docker/overlay2 /var/lib/docker/overlay

## 5. 重启 Docker 并验证驱动
sudo systemctl daemon-reload
sudo systemctl start docker

## 6. 验证存储驱动
docker info | grep "Storage Driver"  # 应显示 "Storage Driver: vfs"

# SSD 挂载问题

##  查看SSD设备信息
sudo fdisk -l

## 安装gparted（用于分区管理）
sudo apt-get install gparted

## 方式 1 （新系统失效）
### 进入overlayroot环境
sudo overlayroot-chroot

### 创建新的挂载点
nano /etc/systemd/system/mnt-MySSD.mount

### 编辑内容
[Unit]
Description=Mount MySSD to /mnt/MySSD
Requires=local-fs.target
After=local-fs.target systemd-udev-settle.service
Before=docker.service

[Mount]
What=/dev/nvme0n1p1  # 用绝对设备路径，避免UUID解析错误
Where=/mnt/MySSD     # 纯本地路径，无/media/root-ro前缀
Type=ext4
Options=rw,defaults,_netdev,nofail,x-systemd.device-timeout=10

[Install]
WantedBy=multi-user.target

### 启用并启动挂载
systemctl enable mnt-MySSD.mount
exit

### 重启验证
reboot
df -h

## 方式 2 （新系统有效）
### 获取SSD的UUID
sudo blkid /dev/nvme0n1p1
### 编辑 rc.local 
sudo nano /etc/rc.local

### 添加挂载命令（替换UUID 和挂载点为你的实际值）
#!/bin/bash

UUID=$(blkid -s UUID -o value /dev/nvme0n1p1)
mount UUID=$UUID /mnt/nvme
exit 0

### 赋予执行权限
sudo chmod +x /etc/rc.local

### 启动rc-local 服务
sudo systemctl enable rc-local
sudo systemctl start rc-local

#  内核加载问题
修改文件内容（提前加载内核模块）：/usr/bin/hobot-loadko.sh

# 验证CAN通讯-lscand工具使用
## 安装can-utils
sudo apt install can-utils
sudo apt install net-tools

## 查看设备文件节点
ls -l /dev/ttyACM*

## 使用slcand来启动串行到CAN的映射，用于设置串行设备为CAN模式
sudo slcand -o -c -s8 -S1000000 /dev/ttyACM0 can0

参数解释：
-o：打开串行设备。

-c：创建一个新的CAN接口。

-s*：（小s）设置CAN波特率
-s0 = 10k
-s1 = 20k
-s2 = 50k
-s3 = 100k
-s4 = 125k
-s5 = 250k
-s6 = 500k
-s7 = 750k
-s8 = 1Mbps

-S*：（大S）设置串口波特率，如-S1000000：设置串口波特率为1Mbps。也可以不设置。

/dev/ttyACM0：作者的串行设备的路径。

can*：新创建的CAN接口的名称，如can0

## 启动CAN接口
sudo ifconfig can0 up

## 监听CAN数据
candump can0

## 使用cansend测试（发送can 报文）
cansend can0 027#04

## 测试结束，关闭CAN接口
sudo ifconfig can0 down

# CAN 通讯验证-CandleLight 固件模式
## 1. 启动 can0 接口，设置 1Mbps 波特率（根据需求调整为 500000 等）
sudo ip link set can0 up type can bitrate 1000000

## 可选：禁用回环模式（如需与外部 CAN 设备通信）
sudo ip link set can0 up type can bitrate 1000000 loopback off

## 2. 验证接口状态（关键）
ip link show can0

## 发送测试 CAN 帧
cansend can0 027#04

## 新开终端接收 CAN 帧（验证是否能监听到）
candump can0




