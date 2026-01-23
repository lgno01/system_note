# build command
imobuilder build driving_control_base -v -r
imobuilder build driving_control_app -v

# run sil (path of target in )
## open one terminator
. ./etc/imo_com/imo_mdw_init.bash
opt/imo_com_service/bin/imo_com_service

## opeb other terminator
. ./etc/imo_com/imo_mdw_init.bash
opt/DrivingControl/bin/DrivingControl

