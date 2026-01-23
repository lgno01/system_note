# Release build for ARM
./idc.sh arm -t apu -p cpj_dflzm -d d100 -v f0b1 -vh m6 -c Release -m full

# ReleaseWithDebugInfo build for ARM
./idc.sh arm -t apu -p cpj_dflzm -d d100 -v f0b1 -vh m6 -c RelWithDebInfo -m full

# sil
./idc.sh sil_gcc -t sil -p cpj_dflzm -d d100 -v f0b1 -vh m6 -c Debug -m full