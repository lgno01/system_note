
cmake_minimum_required(VERSION 3.16)

project(demo)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin) # 设置可执行文件输出路径to bin

# aux_source_directory(. SRC_LIST) # 获取当前目录下的所有源文件
set(SRC_LIST
    ./main.cpp
    ./testFunc.cpp
    ./testFunc1.cpp) # 把指定的源文件加入列表 SRC_LIST中

add_executable(demo ${SRC_LIST})

message(STATUS "Hello world! build sucessful")