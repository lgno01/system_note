
# ROS2 在ubuntu 22.04 的安装

## 1.设置编码
    sudo apt update && sudo apt install locales
    sudo locale-gen en_US en_US.UTF-8
    sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 
    export LANG=en_US.UTF-8

## 2.添加源
    sudo apt update && sudo apt install curl gnupg lsb-release
    sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

## 3.安装ROS2
    sudo apt update
    sudo apt upgrade
    sudo apt install ros-humble-desktop

## 4.设置环境变量
    source /opt/ros/humble/setup.bash
    echo " source /opt/ros/humble/setup.bash" >> ~/.bashrc 

## 5.测试
### 起两个终端，分别运行以下命令
    ros2 run demo_nodes_cpp talker
    ros2 run demo_nodes_py listener
### 实例2,起两个终端,分别运行以下命令,出现海龟仿真器
    ros2 run turtlesim turtlesim_node
    ros2 run turtlesim turtle_teleop_key

## 6.安装 colcon 编译依赖包
    sudo apt install python3-colcon-ros

## 7.安装 colcon 扩展
    sudo apt install python3-colcon-common-extensions 

### 7.1 colcon 常见扩展的说明
    python3-colcon-alias                #提供别名功能，允许用户为常用的colcon命令创建简短的快捷方式。
    python3-colcon-argcomplete                #集成argcomplete库，为colcon命令提供命令行参数自动补全功能。
    python3-colcon-bash                #提供Bash脚本支持，允许colcon在Bash环境中更好地工作。
    python3-colcon-bazel                #为使用Bazel构建系统的项目提供colcon支持。
    python3-colcon-cd                #允许colcon在执行命令前自动切换到指定的工作目录。
    python3-colcon-clean                #提供清理构建产物的功能。
    python3-colcon-cmake                #为使用CMake构建系统的项目提供colcon支持。
    python3-colcon-common-extensions                #包含一些常用的colcon扩展。
    python3-colcon-core                #colcon的核心功能，包括命令行解析、日志记录、工作空间管理等。
    python3-colcon-coveragepy-result                #集成coverage.py，提供代码覆盖率结果的处理和报告功能。
    python3-colcon-defaults                #提供colcon的默认配置和设置。
    python3-colcon-devtools                #提供开发工具支持，如调试和性能分析。
    python3-colcon-ed                #与编辑器集成相关的功能。
    python3-colcon-hardware-acceleration                #提供硬件加速支持，可能涉及GPU或其他加速器。
    python3-colcon-installed-package-information                #提供已安装包的信息查询功能。
    python3-colcon-lcov-result                #集成LCOV，提供代码覆盖率结果的另一种处理和报告方式。
    python3-colcon-library-path                #管理库路径，确保构建和运行时能够找到正确的库文件。
    python3-colcon-meson                #为使用Meson构建系统的项目提供colcon支持。
    python3-colcon-metadata                #管理colcon项目的元数据。
    python3-colcon-mixin                #提供Mixin支持，允许通过组合的方式增强colcon的功能。
    python3-colcon-notification                #提供构建和测试结果的通知功能，可能通过邮件、Slack等渠道发送。
    python3-colcon-output                #管理colcon命令的输出，包括日志、进度信息等。
    python3-colcon-override-check                #检查并报告可能的配置覆盖情况，以避免意外的构建行为。
    python3-colcon-package-information                #提供包信息查询功能，如包的依赖关系、版本等。
    python3-colcon-package-selection                #允许用户选择性地构建和测试项目中的包。
    python3-colcon-parallel-executor                #提供并行执行构建和测试任务的功能，以提高效率。
    python3-colcon-pkg-config                #集成pkg-config，提供包配置信息的查询功能。
    python3-colcon-powershell                #提供PowerShell脚本支持，允许colcon在PowerShell环境中更好地工作。
    python3-colcon-python-setup-py                #为使用Python setup.py构建系统的项目提供colcon支持。
    python3-colcon-recursive-crawl                #提供递归遍历项目目录的功能，以发现更多的包和构建目标。
    python3-colcon-rerun                #允许用户重新运行之前的构建和测试任务。
    python3-colcon-ros                #为ROS2项目提供colcon支持，包括构建、测试、安装等。
    python3-colcon-ros-distro                #提供ROS发行版支持，允许用户根据特定的ROS发行版构建项目。
    python3-colcon-ros-domain-id-coordinator                #在ROS 2项目中协调域ID（Domain ID）的分配和使用。
    python3-colcon-spawn-shell                #允许用户从colcon命令中启动一个新的shell会话。
    python3-colcon-test-result                #处理并报告测试结果，包括测试的成功、失败、跳过等信息。
    python3-colcon-zsh                #提供Zsh脚本支持，允许colcon在Zsh环境中更好地工作。


## 8.安装moveit
    sudo apt install ros-humble-moveit
## 9.自动安装依赖
    sudo apt install -y python3-pip # 安装pip3
    sudo pip3 install rosdepc # 安装rosdepc
    sudo rosdepc init # 初始化 rosdepc
    rosdepc update  # 更新 rosdepc
    cd ..           # 切换到工作空间的根目录
    rosdepc install -i --from-path src --rosdistro humble -y # 自动安装 src 目录下的依赖,对应的ros2版本为 humble

# 编译整个工作空间
    colcon build

# 编译单个package
## 编译一个单独的包
    colcon build --packages-select <name-of-pkg>
    <!-- 但这个指令并不会编译该包的依赖，往往会报错。可以用下面这条指令进行包和其依赖编译 -->
## 编译一个单独的包及其依赖
    colcon build --packages-up-to <name-of-pkg>

# 编译单个文件 并清除之前的编译结果
    colcon build --packages-select <name-of-pkg> --cmake-clean-cache
    <!-- 这条指令会清除该包的编译缓存，然后重新编译该包 -->

# 跳过编译某个包
    colcon build --packages-skip <name-of-pkg>
    <!-- 这条指令会跳过编译该包，但是会编译该包的依赖 -->