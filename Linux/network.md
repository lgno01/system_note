# 虚拟机网卡检测不到
- 1. 尝试 systemctl restart network 重启网卡。如果不成功，报出 Failed to restart network.service: Unit network.service not found 则尝试步骤 2
- 2. nmcli networking off 然后 nmcli networking on 激活网卡