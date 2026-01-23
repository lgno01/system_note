# 文件和目录管理

## 列出目录中的所有文件和子目录
ls
ls -l  # 列出文件的详细信息

## 切换目录
cd
-- cd /home/mydir   # 切换到 home/mydir 目录下
-- cd ..            # 返回上一级目录
-- cd ../..         # 返回上两级目录

## 显示当前工作目录的路径
pwd

## 创建新目录
mkdir
-- mkdir mydir  # 创建名为mydir的目录
-- mkdir -p /home/mydir1/mydir2  # 创建多层目录

## 删除文件或目录
rm -rf mydir    # -r 代表递归删除目录下的文件， -f 强制删除

## 复制文件或目录
cp -rp ./mydir  /home  # -r 递归复制目录下的文件， -p 不改变原有属性，如权限。 把mydir 目录复制到/home 目录下。

## 移动或重命名
mv file ./home     # 移动file文件到home目录下
mv file file_bak   # 把file重命名为 file_bak


# 文件内容查看和处理命令
## 把文件内容打印到终端
cat
cat error.log

## 输出文件内容的末尾到终端, 通常与 -f 或 -n 搭配使用
tail       
-- tail -f error.log           # 实时输出内容
-- tail -n 500 error.log       # 输出error.log 文件最后500行

## 输出文件内容的开头几行
head
-- head -n 30 error.log        # 输出error.log 文件开头30行

## 筛选符合某种文本的内容
grep # 通常和管道符 | 搭配使用
-- cat error.log | grep 18:00  # 打印error.log 中含 18：00 的行 

## 查找文件和目录
find
-- find / -name error.log  # 在 / 根目录下开始查找名为 error.log 的文件

## 比较文件差异
diff
-- diff dm.ini dm_bak.ini      # 比较dm.ini 和dm_bak.ini 的内容差异

# 进程管理命令
## 查看当前进程信息
ps
-- ps -ef             # -e 显示所有进程， -f 使用详细的进程信息

## 实时显示系统中各进程的资源占用情况
top
top -H -p xxx      # 显示PID号为 xxx 的进程中的线程信息

## 终止进程
kill

# 网络管理命令
## 查看网络信息
ifconfig

## 测试网络连接状态
ping 192.168.1.135

## 远程登录
ssh    # ssh root@192.168.1.135

## 远程复制文件
scp        # scp idc_ipark.bin root@172.16.100.13:/opt/idc/bin

# 授权文件
chomd
-- chmod +/-r file   # 添加/删除可读权限
-- chmod +/-w file   # 添加/删除可写权限
-- chmod +/-x file   # 添加/删除可执行权限
-- chmod 777 file    # 等价 chmod a=rwx, 授权所有者/所属组/其他成员，可读、可写、可执行权限。


# 压缩解压命令
-- tar           # 打包和解包文件
-- zip / unzip   # 压缩和解压文件 

# 磁盘空间管理命令
## 查看磁盘空间使用情况
df
## 查看目录或文件占用空间大小
du

## 查看所有块设备信息
lsblk

## 查看分区信息
fdisk -l

## 卸载分区
umount /dev/sdb1

## 给分区自定义标签
sudo e2label /dev/nvme0n1p1 MySSD

# 终端信息输出重定向
imobuilder build driving_control_base -v > xxx.log 2>&1