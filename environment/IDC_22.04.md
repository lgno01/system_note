# 22.04
sudo apt install -y build-essential vim git cmake python3-pip clang-format mono-runtime openjdk-11-jdk openjdk-8-jre-headless mesa-common-dev freeglut3 freeglut3-dev libgles2-mesa-dev libjpeg-dev libpng-dev libdrm-dev llvm clang libc++1 libc++abi1 zsh wget curl libqt5charts5-dev unzip usrmerge zip sshpass libgtk2.0-dev libtinfo5 checkpolicy lz4 ccache flex bison libyaml-dev libssl-dev libc6:i386 libncurses5:i386 libstdc++6:i386

# python
pip3 install gitpython atomicwrites numpy ujson pysmb openpyxl requests -i http://pypi.doubanio.com/simple/ --trusted-host pypi.doubanio.com -U

# qt5
sudo apt install -y qtbase5-dev qt5-qmake libqt5charts5-dev