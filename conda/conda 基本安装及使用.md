
# conda 基本作用和安装
    通用环境管理工具，可以管理不同的python版本，cmake版本，c++ 编译器版本等。
# conda 基本操作
## 创建新环境
    conda create --name myenv python=3.10
    - myenv 为你希望的环境名
    - python 指定python版本

## 激活已有环境
    conda activate myenv

## 退出环境
    conda deactivate

## 查看本地环境列表
    conda env list

## 删除环境
    conda remove --name myenv --all

## 安装包
    conda install numpy=1.18.5
    - 默认安装最新版本的包，可以指定版本号安装
## 更新包
    conda update numpy
## 卸载包
    conda remove numpy
## 查看已安装的包
    conda list

## 查看conda 配置信息
    conda info