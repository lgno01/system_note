 # Release
 ./idc.sh arm -t apu -p cpj_chery -d d300 -v d2b5 -vh e0x -c Release -m full

# RelWIthDebInfo
 ./idc.sh arm -t apu -p cpj_chery -d d300 -v d2b5 -vh e0x -c RelWithDebInfo -m full

# sil
./idc.sh sil_gcc -t sil -p cpj_chery -d d300 -v d2b5 -vh e0x -c Debug -m full
 


# 刷软件
--网线ip设置: 192.168.1.199
--板子：ssh root@192.168.1.135 
--密码：Holo@91320
--换bin: mount -o remount rw /opt/
--ipark目录: /opt/idc/bin/