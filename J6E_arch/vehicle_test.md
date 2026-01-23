# connect to idc
- ssh root@192.168.1.100

# copy app to idc
- scp scp -r xxx root@192.168.1.100:/opt/idc

# check all apps status(path: /opt/idc)
- ./run.sh status all
