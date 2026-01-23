# config 仓库定义了所有的仓库地址和对应的依赖关系，但并不是所有的仓库都有权限。应该是通过config 这些配置来管理src中的仓库
# driving_control_base 在config 中的依赖关系已经配置好。编译driving_control_base时，可直接使用 imobuilder build driving_control_base -v -r 指令
# 更新依赖库，imobuilder init driving_control_base -r

# 编译driving_control 时，需要先编译driving_control_base，再执行 imobuilder build driving_control -v 不要加 -r ,因为imo_com 没有权限。


# swarch_config 仓库定义进程和线程间的通信接口，app内的部分代码也是根据其生成的。
    - swc 中定义每个swc 的输入输出（进程间通信接口）（port口名字可自定义，但一定要绑定event 中的event名字）
    - event 定义总线上的事件，即每个swc 向外发送的port
    - executable 定义每个进程的线程结构，接口等。

# 遇到类似于 imoapp command not found 的问题，尝试以下指令
    - imobuilder clean imoapp_bin
    - imobuilder build imoapp_bin

# 20.04的系统配置了22.04 的编译平台，导致 GLIBCXX_3.4.29' not found 问题，解决方法如下：
    - sudo apt update
    - sudo apt upgrade libstdc++6
