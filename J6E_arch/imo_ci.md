# ci 
https://ci.imotion.ai/workspace

# output about
   BSW_ARCH
# ci download output setting
1. imobuilder configure  ci_service.token=<your_token> ; <your_token>为字符串需要用" "包含;
   token can change,so remeber update.

2. imobuilder configure  ci_service.url=https://ci.imotion.ai
   build_id 即为ci web上的构建任务的id号
3. imobuilder download --build_id xxx

4. 下载target之后删除一下download的缓存文件，否则会导致缓存存在无法编译repo
   rm <workspace>/output/<build_platform>/<build_type>/dowload/*

5. no imoapp in ci output target, should build imoapp for every platform and build_type
   imobuilder build imoapp_bin