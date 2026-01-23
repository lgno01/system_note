# Release
./idc.sh arm -t apu -p cpj_chery -d d300e -v d3b6 -vh v2x -c Release -m full 
# Debug
./idc.sh arm -t apu -p cpj_chery -d d300e -v d3b6 -vh v2x -c Debug -m full 
# RelWithDebInfo
./idc.sh arm -t apu -p cpj_chery -d d300e -v d3b6 -vh v2x -c RelWithDebInfo -m full

# xmt sil
./idc.sh sil_gcc -t sil -p cpj_chery -d d300e -v d3b6 -vh v2x -c Debug -m full