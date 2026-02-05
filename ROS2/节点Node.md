
# 创建节点流程
rcl代表ros client library(ros 客户端库)
## 1. 编程接口初始化
- 初始化ROS2 C++接口
    - rclcpp::init(argc, argv);
- 初始化ROS2 Python接口
    - rclpy.init(args=None)

## 2. 创建节点对象，进行初始化
- C++ 创建节点对象
    - auto node = std::make_shared<<NodeClassName>>();
- Python 创建节点对象
    - node = rclpy.Node(<node_name>)

## 2. 实现节点功能
- C++ 实现节点功能
    - rclcpp::spin(node);
- Python 实现节点功能
    - rclpy.spin(node)
## 3. 销毁节点对象
- C++ 销毁节点对象
    - node.reset();
- Python 销毁节点对象
    - node.destroy_node()
## 4. 关闭编程接口
- C++ 关闭编程接口
    - rclcpp::shutdown();
- Python 关闭编程接口
    - rclpy.shutdown()
