# Debug
./idc.sh arm -t apu -p cpj_jxev -d d500 -v h0c2 -vh pf1 -c Debug -m full
# Release
./idc.sh arm -t apu -p cpj_jxev -d d500 -v h0c2 -vh pf1 -c Release -m full
# RelWithDebInfo
./idc.sh arm -t apu -p cpj_jxev -d d500 -v h0c2 -vh pf1 -c RelWithDebInfo -m full

# mcu
./idc.sh arm -t rpu -p cpj_jxev -d d500 -v h0c2 -vh pf1 -c Debug -m full -cr 10

# sil
./idc.sh sil_gcc -t sil -p cpj_jxev -d d500 -v h0c2 -vh pf1 -c Debug -m full