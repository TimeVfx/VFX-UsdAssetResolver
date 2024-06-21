# Requirements [依赖需求]

## System dependencies [系统依赖]
Currently building on Linux and Windows is documented. We use CMake as our build system and link against Houdini/Maya to avoid having to compile our own version of Usd.

[ 当前在 Linux 和 Windows 上的构建已被记录. 我们使用 CMake 作为构建系统并链接到 Houdini/Maya，以避免编译我们自己的 Usd 版本]

It is also possible to compile against a self-compiled Usd build, this is not covered by this guide though.

[ 也可以针对自编译的 USD 版本进行编译，但这并不包含在本指南中]

VFX DCC vendors try to keep in sync with the versions specified in the [VFX Reference Platform](https://vfxplatform.com), so if something doesn't work, first make sure that your software versions are supported.

[ VFX DCC 供应商尝试与 [VFX Reference Platform](https://vfxplatform.com) 中指定的版本保持同步，因此如果出现问题，请首先确保您的软件版本受支持]

```admonish warning
Since the Usd Asset Resolver API changed with the AR 2.0 standard proposed in the [Asset Resolver 2.0 Specification](https://openusd.org/release/wp_ar2.html), you can only compile against Houdini versions 19.5 and higher/Maya versions 2024 and higher.

[ 由于 Usd Asset Resolver API 随 Asset Resolver 2.0 规范中提出的 AR 2.0 标准而更改，因此您只能针对 Houdini 版本 19.5 及更高版本/Maya 2024 及更高版本进行编译]
```

## Linux
```admonish success title=""
| Software               | Website                                                                | Min (Not Tested)     | Max (Tested)  |
|------------------------|------------------------------------------------------------------------|----------------------|---------------|
| gcc                    | [https://gcc.gnu.org](https://gcc.gnu.org/)                            | 11.2.1               | 13.1.1        |
| cmake                  | [https://cmake.org](https://cmake.org/)                                | 3.26.4               | 3.26.4        |
| SideFX Houdini         | [SideFX Houdini](https://www.sidefx.com)                               |  19.5                | 19.5          |
| Autodesk Maya          | [Autodesk Maya](https://www.autodesk.com/ca-en/products/maya/overview) |  2024                | 2024          |
| Autodesk Maya USD SDK  | [Autodesk Maya USD SDK](https://github.com/Autodesk/maya-usd)          |  0.27.0              | 0.27.0        |
```

## Windows
```admonish success title=""
| Software               | Website                                                                            | Min (Not Tested)     | Max (Tested)  |
|------------------------|------------------------------------------------------------------------------------|----------------------|---------------|
|Visual Studio 16 2019   | [https://visualstudio.microsoft.com/vs/](https://visualstudio.microsoft.com/vs/)   | 11.2.1               | 13.1.1        |
| cmake                  | [https://cmake.org](https://cmake.org/)                                            | 3.26.4               | 3.26.4        |
| SideFX Houdini         | [SideFX Houdini](https://www.sidefx.com)                                           |  19.5                | 19.5          |
| Autodesk Maya          | [Autodesk Maya](https://www.autodesk.com/ca-en/products/maya/overview)             |  2024                | 2024          |
| Autodesk Maya USD SDK  | [Autodesk Maya USD SDK](https://github.com/Autodesk/maya-usd)                      |  0.27.0              | 0.27.0        |
```

When compiling against Houdini/Maya on Windows, make sure you use the Visual Studio version that Houdini/Maya was compiled with as noted in the [HDK](https://www.sidefx.com/docs/hdk/_h_d_k__intro__getting_started.html#HDK_Intro_Compiling_Intro_Windows)/[SDK](https://github.com/Autodesk/maya-usd). You'll also need to install the [Visual Studio build tools](https://visualstudio.microsoft.com/downloads/?q=build+tools) that match the Visual Studio release if you want to run everything from the terminal.

[ 在 Windows 上针对 Houdini/Maya 进行编译时，请确保您使用的是与 Houdini/Maya 编译时所用的 Visual Studio 版本保持一致，具体请参照 HDK/SDK 中的说明. 如果您希望从终端运行所有内容，您还需要安装与 Visual Studio 发行版相匹配的 [Visual Studio 构建工具](https://visualstudio.microsoft.com/downloads/?q=build+tools)]