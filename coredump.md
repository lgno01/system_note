# 1. 对启动文件进行更改（startup_app.sh）,添加以下内容
    rm -rf /mnt/coredump
    mkdir /mnt/coredump
    echo "/mnt/coredump/core-%e-%p-%t" > /proc/sys/kernel/core_pattern
    ulimit -c unlimited

# 2. 解析
    2.1 进入IDC硬件coredump文件存放目录， cd mnt/coredump
    2.2 执行ls命令，查看coredump文件
    2.3 运行指令： gdb /opt/idc/bin/idc_ipilot.bin ./core-idc_ipilot.bin-xxx 解析coredump文件
    2.4 输入命令：where，查看当前执行位置
    2.5 bt，查看堆栈信息
