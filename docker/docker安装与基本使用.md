# docker 安装与配置
## 安装docker
  https://docs.docker.com/engine/install/ubuntu/

## 验证docker是否安装成功
  sudo docker run hello-world

## 修改docker用户组，无需sudo执行
### 1. 创建docker用户组
  sudo groupadd docker

### 2. 添加当前用户加入docker用户组
  sudo usermod -aG docker ${USER}

### 3. 重启docker服务
sudo systemctl restart docker

### 4、生效配置
sudo newgrp docker

## 修改docker数据目录
### 1. 查看当前docker数据目录
  sudo docker info | grep "Docker Root Dir"

### 2. 创建新的docker数据目录
  sudo mkdir xxx/docker

### 3. 修改docker配置文件
  mkdir -p /etc/systemd/system/docker.service.d/
  vi /etc/systemd/system/docker.service.d/devicemapper.conf
#### 添加以下内容
  [Service]
  ExecStart=
  ExecStart=/usr/bin/dockerd  --data-root=xxx/docker

### 4.设置正确的属主和权限（Docker 进程以 root 运行，需确保权限足够）
  sudo chown root:root xxx/docker
  sudo chmod 700 xxx/docker
### 5.重启docker服务
#### 重新加载 systemd 配置
  sudo systemctl daemon-reload
#### 重启 Docker 服务
  sudo systemctl restart docker
#### 验证 Docker 是否正常运行
  sudo systemctl status docker

## docker 网络配置
### 1. 将 iptables 切换到 legacy 模式
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy

### 2. 确认切换成功（输出应显示 "legacy"）
update-alternatives --list iptables

### 3. 重新启动 Docker 服务
sudo systemctl restart docker

### 4. 检查 Docker 服务状态
sudo systemctl status docker

### 5. 验证 iptables 工作模式
sudo update-alternatives --query iptables

## 切换docker存储驱动
### 1. 停止 Docker 服务
sudo systemctl stop docker
sudo systemctl stop docker.socket

### 2. 备份原有 Docker 配置（如有）
sudo cp /etc/docker/daemon.json /etc/docker/daemon.json.bak 2>/dev/null || true

### 3. 配置 vfs 存储驱动
sudo tee /etc/docker/daemon.json <<EOF
{
  "storage-driver": "vfs"
}
EOF

### 4. 清理旧存储驱动残留（可选，避免冲突）
sudo rm -rf /var/lib/docker/overlay2 /var/lib/docker/overlay

### 5. 重启 Docker 并验证驱动
sudo systemctl daemon-reload
sudo systemctl start docker

### 6. 验证存储驱动
docker info | grep "Storage Driver"  # 应显示 "Storage Driver: vfs"

## 绕过网络依赖
### 1. 停止 Docker 服务
sudo systemctl stop docker
sudo systemctl disable docker # 禁用docker服务自动启动

### 2. 创建、修改 docker 配置文件
<!-- # 创建 Docker 配置目录（确保存在） -->
sudo mkdir -p /etc/docker

<!-- # 编辑 daemon.json 配置文件（核心：禁用默认桥接网络） -->
sudo tee /etc/docker/daemon.json > /dev/null <<EOF
{
  "bridge": "none",
  "iptables": false,
  "ip-masq": false,
  "ipv6": false,
  "experimental": false,
  "storage-driver": "vfs"
}
EOF

### 3 重新加载并启动docker服务
<!-- # 重新加载 systemd 配置 -->
sudo systemctl daemon-reload

<!-- # 启动 Docker 服务 -->
sudo systemctl enable --now docker

<!-- # 查看 Docker 状态（验证是否启动成功） -->
sudo systemctl status docker


# docker 常见命令
  
## docker 的启动、重启与状态查看
### 启动docker
  sudo systemctl start docker

### 重启docker
  sudo systemctl restart docker

### 查看docker状态
  sudo systemctl status docker

## docker 日志与基本信息查看
### 查看最近docker 日志
  sudo journalctl -n 100 -u docker

### 查看docker 信息（可用容量，版本，数据路径等）
  sudo docker info

## docker 镜像操作

### 加载tar包镜像
sudo docker load -i xxx.tar

### 从远端拉取镜像
docker login <registry_url> # 如 docker login --username=gang.li@69543705 imotion-cn-beijing.cr.volces.com，登录镜像仓库
sudo docker pull <image_name>:<tag> # 如 docker pull imotion-cn-beijing.cr.volces.com/robot/irc_li_auto_x86:20251225，
<!--  其中 imotion-cn-beijing.cr.volces.com 为镜像仓库地址，robot 为镜像仓库命名空间，irc_li_auto_x86 为镜像名称，20251225 为镜像标签; 如果不指定仓库地址，默认从 Docker Hub 拉取 -->

### 查看镜像列表
sudo docker images

### 查看镜像详细信息
sudo docker inspect <image_id>

### 删除docker 镜像
sudo docker rmi <image_id>

### 保存docker镜像更改(并创建新的镜像)
docker ps -a # 查看所有容器
docker commit -m "xxx" <container_id> <image_name>:<tag>

### 保存docker镜像为tar包
sudo docker save -o xxx.tar <image_name>

### 推送镜像到远端仓库
docker login <registry_url> # 如 docker login --username=gang.li@69543705 imotion-cn-beijing.cr.volces.com，登录镜像仓库
docker push <image_name>:<tag> # 如 docker push imotion-cn-beijing.cr.volces.com/robot/irc_li_auto_x86:20251225，
<!--  其中 imotion-cn-beijing.cr.volces.com 为镜像仓库地址，robot 为镜像仓库命名空间，irc_li_auto_x86 为镜像名称，20251225 为镜像标签; 如果不指定仓库地址，默认从 Docker Hub 推送 -->

## docker 容器操作
### 查看docker 所有容器
sudo docker ps -a

### 进入同一个网络下的容器
sudo docker exec -it <container_id> bash

## 查看 dockerd 进程的启动参数
ps aux | grep dockerd | grep -v grep

##  停止容器
sudo docker stop xxx

## 删除容器
sudo docker rm xxx

# docker 清理
## 查看docker 磁盘占用情况
sudo docker system df

## 删除停止的容器、悬空镜像、未被使用的网络
sudo docker system prune -f

## 清理所有未使用的镜像、容器、卷和网络（-a 表示所有未使用的镜像，--volumes 表示删除所有未使用的卷）
sudo docker system prune -a --volumes -f

## 清理未使用的镜像
sudo docker image prune -a -f



