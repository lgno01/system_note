# 创建功能包
ROS2 功能包（package）使用文档 — 快速指南


1. 创建功能包
- C++ (ament_cmake)：
    ros2 pkg create --build-type ament_cmake <pkg_name> --dependencies rclcpp std_msgs
- Python (ament_python)：
    ros2 pkg create --build-type ament_python <pkg_name> --dependencies rclpy std_msgs

2.编译功能包
- 在工作空间根目录下运行：
    colcon build --packages-select <pkg_name>  # 编译指定包
    colcon build                            # 编译所有包
    colcon build --packages-up-to <pkg_name>  # 编译指定包及其依赖

3. 功能包结构
- C++ (ament_cmake) 包：
    - package.xml                      # 包描述文件
    - CMakeLists.txt                   # 构建配置文件
    - src/                             # C++ 源码或节点
    - include/<pkg_name>/              # C++ 头文件
    - msg/, srv/, action/              # 自定义消息/服务/动作定义
    - launch/                          # launch 文件（Python）
    - test/                            # 单元/集成测试
    - README.md
    - cfg/                             # 参数描述（可选）
- Python (ament_python) 包：
    - package.xml                      # 包描述文件
    - setup.py                         # 构建配置文件
    - setup.cfg                        # 安装配置文件
    - resources/                       # 资源文件（如入口点）
    - <pkg_name>/                      # Python 源码或节点
    - msg/, srv/, action/              # 自定义消息/服务/动作定义
    - launch/                          # launch 文件（Python）
    - test/                            # 单元/集成测试
    - README.md
    - cfg/                             # 参数描述（可选） 

