#Cmake 最低版本号要求
cmake_minimum_required(VERSION 2.8)

# 项目信息
project (Demo)

# 查找目录下的所有源文件
# 并将名称保存到DIR_SRCS变量
aux_source_directory(. DIR_SRCS)
#aux_source_directory(${PROJECT_SOURCE_DIR}/../include direct3dinclude)
include_directories(../include)

# 设置子系统为窗口程序
set ( CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /SUBSYSTEM:WINDOWS" ) 

#项目使用UNICODE版本。win中的各种API将使用UNICODE版本。
add_definitions("-DUNICODE" "-D_UNICODE")
link_directories(${PROJECT_SOURCE_DIR}/../Lib/x86)
#link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../Lib/x86)


# 指定生成目标
add_executable(Demo ${DIR_SRCS})

# 添加链接库
target_link_libraries(Demo d3d9.lib d3dx10.lib d3dx9.lib dxerr.lib dxguid.lib winmm.lib comctl32.lib)
