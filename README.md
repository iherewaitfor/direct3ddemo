# Direct3D9 demo

# 环境搭建
先去下载[DirectX Software Development Kit](https://www.microsoft.com/en-us/download/confirmation.aspx?id=6812)。本文写时下载到的地址[https://download.microsoft.com/download/A/E/7/AE743F1F-632B-4809-87A9-AA1BB3458E31/DXSDK_Jun10.exe](https://download.microsoft.com/download/A/E/7/AE743F1F-632B-4809-87A9-AA1BB3458E31/DXSDK_Jun10.exe)。下载下来的文件DXSDK_Jun10.exe。

## include
include文件夹放的是Direct3D的相关头文件。是从安装DXSDK_Jun10.exe的目录的include文件夹中复制过来的。
## Lib
Lib文件夹放的是Direct3D的相关头文件。是从安装DXSDK_Jun10.exe的目录的Lib文件夹中复制过来的。

# CreateDevice Demo
该项目中主用于验证工程配置。以及运行最基本的Dirtect3D9的程序。

## HOW TO RUN
安装好cmake。进入到CreateDevice中创建build目录，然后执行cmake命令

cmake .. -G "Visual Studio 17 2022" -A Win32

然后在build中就能看到Demo.sln文件，打开编译运行即可。
```
D:\srccode\direct3ddemo\CreateDevice\build>cmake .. -G "Visual Studio 17 2022" -A Win32
CMake Deprecation Warning at CMakeLists.txt:2 (cmake_minimum_required):
  Compatibility with CMake < 2.8.12 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Selecting Windows SDK version 10.0.22621.0 to target Windows 10.0.19045.
-- The C compiler identification is MSVC 19.33.31630.0
-- The CXX compiler identification is MSVC 19.33.31630.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.33.31629/bin/Hostx64/x86/cl.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.33.31629/bin/Hostx64/x86/cl.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: D:/srccode/direct3ddemo/CreateDevice/build

D:\srccode\direct3ddemo\CreateDevice\build>
```