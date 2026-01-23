# Release
./idc.sh arm -t apu -p cpj_chery -d d300e -v d3b6 -vh pf1 -c Release -m full 
# Debug
./idc.sh arm -t apu -p cpj_chery -d d300e -v d3b6 -vh pf1 -c Debug -m full 
# RelWithDebInfo
./idc.sh arm -t apu -p cpj_chery -d d300e -v d3b6 -vh pf1 -c RelWithDebInfo -m full

# mcu
./idc.sh arm -t rpu -p cpj_chery -d d300e -v d3b6 -vh pf1 -c Debug -m full -cr 10

# sil
./idc.sh sil_gcc -t sil -p cpj_chery -d d300e -v d3b6 -vh pf1 -c Debug -m full

