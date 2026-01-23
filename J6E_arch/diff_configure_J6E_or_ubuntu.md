# J6E debug
imobuilder configure --build_platform aarch64-linux-j6e-zos
imobuilder configure --build_product ZOS/develop
imobuilder configure --build_type debug

# J6E release
imobuilder configure --build_platform aarch64-linux-j6e-zos
imobuilder configure --build_product ZOS/develop
imobuilder configure --build_type release

# 22.04 debug
imobuilder configure --build_platform x86_64-linux-ubuntu-22.04.5-base
imobuilder configure --build_product ZOS/develop
imobuilder configure --build_type debug

# 22.04 release
imobuilder configure --build_platform x86_64-linux-ubuntu-22.04.5-base
imobuilder configure --build_product ZOS/develop
imobuilder configure --build_type release

# 22.04 opengl_cuda_11.8 debug
imobuilder configure --build_platform x86_64-linux-ubuntu-22.04.5-opengl-cuda-11.8
imobuilder configure --build_product ZOS/develop
imobuilder configure --build_type debug

# 22.04 opengl_cuda_11.8 release
imobuilder configure --build_platform x86_64-linux-ubuntu-22.04.5-opengl-cuda-11.8
imobuilder configure --build_product ZOS/develop
imobuilder configure --build_type release


# download crosstools
imobuilder download --crosstool