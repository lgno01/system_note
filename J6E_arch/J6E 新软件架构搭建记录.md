# 工具介绍

## imobuilder
    中间安装不成功，因为python版本不对应，需使用指定的python3.8/python3.10。 我本地电脑为python3.8和python3.13,使用python3 指令默认使用python3.13版本，故失败。后改用python 指令成功。
### 常用功能
    - create 创建工作空间
    - delete 销毁工作空间
    - show 显示工作空间信息
    - configure 配置工作空间
    - init 初始化模块源代码
    - update 更新模块源代码或配置文件
    - build 编译模块
    - clean 清理编译结果、中间文件
    - runspec 使用spec文件创建编译任务
    
    - download 下载资源
    - check 检查配置文件错误
    - package 打包编译结果
    - compare 比较json文件差异
    - export 导出spec文件
    - import 导入spec文件
    - launch 启动ide打开工程
    
## zosidl
    idl 接口定义工具

# 工作空间目录及内容
    - .imobuilder

    - config
      - platform
      - product
      - resources
      - type

    - src  源代码
    
    - build 编译中间产物
      - build/xxx(编译平台)/xxx(编译类型)/编译工程
    
    - output 编译结果
      - output/xxx(编译平台)/xxx(编译类型)/编译结果分类
    
    - crosstool 交叉编译工具链
    
    - package 管理工程包文件和任务包文件
      - 工程包
      - 任务包：
    
    - log 编译过程日志
      - imobuilder.log  imobuilder 工具运行过程中的详细日志

# 产品编译流程
## 创建工作空间
    先创建文件夹，使用imobuilder工具把文件夹配置成工作空间

## 配置工作空间参数
### 配置编译平台-platform
    -X86
    -X86_64
    -ubuntu

### 配置编译类型-build_type
    - release
    - debug
    - Relwithdebinfo

### 配置编译产品信息
    - 源码配置信息（git url, 分支信息等）
    - 编译流程信息（编译命令，编译参数，环境变量等）
    - 依赖关系等

## 初始化各个工程源代码

## 执行产品编译