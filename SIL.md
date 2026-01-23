# 配置launch 文件，其中不同项目，program cwd 需要修改
"version": "0.2.0",
    "configurations": [
        {
            "name": "GDB: run_ipilot",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build/cpj_chery_pf1_d300e_d3b6/sil_gcc/install/bin/idc_xipilotd.bin", // debug
            "args": [
                // "-sim"
            ],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}/build/cpj_chery_pf1_d300e_d3b6/sil_gcc/install",
            "environment": [
                {
                    "name": "LD_LIBRARY_PATH",
                    "value": "/usr/lib/x86_64-linux-gnu:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/sysroot/lib/:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/sysroot/usr/lib/:/home/${env:USERNAME}/Renesas/rcar-xos/v3.18.0/sw/x86_64-gnu-linux/lib:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/sysroot/usr/ext/lib/:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/was/adcc/lib:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/was/log4cplus-3.0/lib:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/was/yaml-cpp-0.8.0/lib:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/was/mozjpeg-0.2.0/lib:/home/${env:USERNAME}/zx/zx_idc_sdk_general/platform/x86_64-linux/was/hobot_adas_sdk_1.0.0/lib/"
                }
            ],
            "externalConsole": false,
            // "preLaunchTask": "build_ipilot_debug", // debug
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        },


# run and debug 运行即可