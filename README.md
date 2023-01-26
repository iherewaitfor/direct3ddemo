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

然后在build中就能看到Demo.sln文件，设置Demo项目为启动项目，打开编译运行即可。
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

## Direct3DCreate9
[Direct3DCreate9](https://learn.microsoft.com/en-us/windows/win32/api/d3d9/nf-d3d9-direct3dcreate9)
```C++
IDirect3D9 * Direct3DCreate9(
  UINT SDKVersion
);
```
SDKVersion

Type: UINT

The value of this parameter should be D3D_SDK_VERSION.

If successful, this function returns a pointer to an IDirect3D9 interface; otherwise, a NULL pointer is returned.

The Direct3D object is the first Direct3D COM object that your graphical application needs to create and the last object that your application needs to release. Functions for enumerating and retrieving capabilities of a device are accessible through the Direct3D object. This enables applications to select devices without creating them.

Create an IDirect3D9 object as shown here:
```C++
LPDIRECT3D9 g_pD3D = NULL;
    
if( NULL == (g_pD3D = Direct3DCreate9(D3D_SDK_VERSION)))
    return E_FAIL;
```
The IDirect3D9 interface supports enumeration of active display adapters and allows the creation of [IDirect3DDevice9](https://learn.microsoft.com/en-us/windows/desktop/api/d3d9helper/nn-d3d9helper-idirect3ddevice9) objects. If the user dynamically adds adapters (either by adding devices to the desktop, or by hot-docking a laptop), those devices will not be included in the enumeration. Creating a new IDirect3D9 interface will expose the new devices.

D3D_SDK_VERSION is passed to this function to ensure that the header files against which an application is compiled match the version of the runtime DLL's that are installed on the machine. D3D_SDK_VERSION is only changed in the runtime when a header change (or other code change) would require an application to be rebuilt. If this function fails, it indicates that the header file version does not match the runtime DLL version.

# Direct3d9渲染管线

![Image Direct3d9渲染管线](./images/blockdiag-graphics.png)

|Pipeline Component|Description|Related Topics|
|:--|:--|:--|
|Vertex Data|Untransformed model vertices are stored in vertex memory buffers.|[Vertex Buffers (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/vertex-buffers) ,[IDirect3DVertexBuffer9](https://learn.microsoft.com/en-us/windows/win32/api/d3d9helper/nn-d3d9helper-idirect3dvertexbuffer9)|
|Primitive Data	|Geometric primitives, including points, lines, triangles, and polygons, are referenced in the vertex data with index buffers.|[Index Buffers (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/index-buffers),[IDirect3DIndexBuffer9](https://learn.microsoft.com/en-us/windows/desktop/api), [Primitives](https://learn.microsoft.com/en-us/windows/win32/direct3d9/primitives), [Higher-Order Primitives (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/higher-order-primitives)|
|Tessellation|The tesselator unit converts higher-order primitives, displacement maps, and mesh patches to vertex locations and stores those locations in vertex buffers.|[Tessellation (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/tessellation)|
|Vertex Processing|Direct3D transformations are applied to vertices stored in the vertex buffer.|[Vertex Pipeline (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/vertex-pipeline)|
|Geometry Processing|Clipping, back face culling, attribute evaluation, and rasterization are applied to the transformed vertices.|[Pixel Pipeline (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/pixel-pipeline)|
|Textured Surface|Texture coordinates for Direct3D surfaces are supplied to Direct3D through the [IDirect3DTexture9](Texture coordinates for Direct3D surfaces are supplied to Direct3D through the IDirect3DTexture9 interface.) interface.|[Direct3D Textures (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/direct3d-textures), [IDirect3DTexture9](https://learn.microsoft.com/en-us/windows/win32/api/d3d9helper/nn-d3d9helper-idirect3dtexture9)|
|Texture Sampler|Texture level-of-detail filtering is applied to input texture values.|[Direct3D Textures (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/direct3d-textures)|
|Pixel Processing|Pixel shader operations use geometry data to modify input vertex and texture data, yielding output pixel color values.|[Pixel Pipeline (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/pixel-pipeline)|
|Pixel Rendering|Final rendering processes modify pixel color values with alpha, depth, or stencil testing, or by applying alpha blending or fog. All resulting pixel values are presented to the output display.|[Pixel Pipeline (Direct3D 9)](https://learn.microsoft.com/en-us/windows/win32/direct3d9/pixel-pipeline)|
