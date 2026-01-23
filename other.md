# 本机设置：
    千兆：IPV4: 192.168.0.xxx
    百兆：IPV4: 192.168.1.xxx

# IDCH ip: 192.168.0.2
# 获取板子控制权：ssh root@192.168.0.2 (千兆) 192.168.1.100 （百兆）
# 杀死程序(根据进程名)：pkill idc
# 拷贝库到板子：scp -r holo_lib/* root@192.168.0.2:/usr/ext/lib/
# 手动启程序：
          ./idc.sh.bak -local 5   (cpf + ipilot)
          ./idc.sh.bak -local 69 （vial + cpf + ipilot）;
          ./idc.sh.bak -local 197 (dalo + vial + cpf + ipilot)
# 清理内存：ipcrm -M 6666 
# 更新：sync

# xmt 环境配置：
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/ligang/zx/zx_idc_sdk_general/platform/x86_64/usr/lib
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/ligang/zx/zx_idc_sdk_general/platform/x86_64-linux/sysroot/usr/ext/lib


# 查看自研感知标定参数
1. signal view
2. ocaloutputv13
3. roll（0.008726599626243114）, pith（0.015438400208950043）, yaw（0.04517989978194237） 的值


# 查看进程信息
1. top 查看所有进程
2. top -H -p xxx 查看pid 为xxx 的进程，会详细显示进程中线程信息
3. 
