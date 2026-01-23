# Release
 ./idc.sh arm -t apu -p cpj_xpht -d d500_x3 -v h3c3 -vh x3 -c Release -m full 

# RelWIthDebInfo
 ./idc.sh arm -t apu -p cpj_xpht -d d500_x3 -v h3c3 -vh x3 -c RelWithDebInfo -m full

# sil
./idc.sh sil_gcc -t sil -p cpj_xpht -d d500_x3 -v h3c3 -vh x3 -c Debug -m full
