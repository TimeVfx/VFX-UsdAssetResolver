# Building [构建]
Currently we support building against Houdini and Maya on Linux and Windows. If you don't want to self-compile, you can also download pre-compiled builds on our [release page](https://github.com/LucaScheller/VFX-UsdAssetResolver/releases). To load the resolver, you must specify a few environment variables, see our [Resolvers > Environment Variables](../resolvers/overview.md#environment-variables) section for more details.

[ 目前，我们支持在 Linux 和 Windows 上针对 Houdini 和 Maya 进行构建. 如果您不想自编译，也可以在我们的 [发布页面](https://github.com/LucaScheller/VFX-UsdAssetResolver/releases) 下载预编译版本. 要加载解析器，您必须指定一些环境变量，请参阅我 [Resolvers > Environment Variables](../resolvers/overview.md#environment-variables) 了解更多详细信息]

## Setting up our build environment [设置我们的构建环境]
After installing the [requirements](./requirements.md), we first need to set a couple of environment variables that our cmake file depends on.

[ 安装 [需求依赖](./requirements.md) 后，我们首先需要设置 cmake 文件所依赖的几个环境变量]

### Using our convenience setup script [使用我们的便捷设置脚本]
On Linux we provide a bash script that you can source that sets up our development environment. This sets a few environment variables needed to build the resolver as well as for Houdini/Maya to load it.
This can be done by running the following from the source directory:

[ 在Linux上，我们提供了一个bash脚本，您可以运行它来设置我们的开发环境. 这将设置构建解析器以及让 Houdini/Maya 加载它所需的一些环境变量.这可以通过在源代码目录中运行以下命令来完成]
~~~admonish info title=""
```bash
source setup.sh
```
~~~

In the [setup.sh](https://github.com/LucaScheller/VFX-UsdAssetResolver/blob/main/setup.sh) file you can define what resolver to compile by setting the `RESOLVER_NAME` variable to one of the resolvers listed in [resolvers](../resolvers/overview.md) in camelCase syntax (for example `fileResolver` or `pythonResolver`). Here you'll also have to define what Houdini/Maya version to compile against.

[ 在 [setup.sh](https://github.com/LucaScheller/VFX-UsdAssetResolver/blob/main/setup.sh) 文件中，您可以通过将 RESOLVER_NAME 变量设置为 [resolvers](../resolvers/overview.md) 中列出的解析器之一（使用驼峰命名法，例如 fileResolver 或 pythonResolver ）来定义要编译的解析器. 在此文件中，您还需要定义要针对哪个 Houdini/Maya 版本进行编译]

It will then automatically set the `PATH`, `PYTHONPATH`, `PXR_PLUGINPATH_NAME` and `LD_LIBRARY_PATH` environment variables to the correct paths so that after your run the compile, the resolver will be loaded correctly (e.g. if you launch Houdini via `houdinifx`, it will load everything correctly). The build process also logs this information again.

[ 随后，它将自动将 PATH、PYTHONPATH、PXR_PLUGINPATH_NAME 和 LD_LIBRARY_PATH 环境变量设置为正确的路径，以便在编译运行后，解析器能够正确加载（例如，如果您通过 houdinifx 启动 Houdini，它将正确加载所有内容）构建过程也会再次记录这些信息]

By default it also sets the `TF_DEBUG` env var to `AR_RESOLVER_INIT` so that you'll get logs of what resolver is loaded by USD's plugin system, which you can use to verify that everything is working correctly.

[ 默认情况下，它还会将 TF_DEBUG 环境变量设置为 AR_RESOLVER_INIT，这样您就可以获取 USD 插件系统加载的解析器日志，您可以使用这些日志来验证一切是否工作正常]

### Manually setting up the environment [手动设置环境]
If you don't want to use our convenience script, you can also setup the environment manually.

[ 如果您不想使用我们的便捷脚本，您也可以手动设置环境]

~~~admonish info title=""
```bash
# Linux
## Houdini
export AR_DCC_NAME=houdini
export HFS=<PathToHoudiniRoot> # For example "/opt/hfs<HoudiniVersion>"
## Maya
export AR_DCC_NAME=maya
export MAYA_USD_SDK_ROOT="/path/to/maya/usd/sdk/root/.../mayausd/USD"
export MAYA_USD_SDK_DEVKIT_ROOT="/path/to/maya/usd/sdk/root/.../content/of/devkit.zip"
export PYTHON_ROOT="/path/to/python/root"
## Resolver
export AR_RESOLVER_NAME=fileResolver

# Windows
## Houdini
set AR_DCC_NAME=houdini
set HFS=<PathToHoudiniRoot> # For example "C:\Program Files\Side Effects Software\<HoudiniVersion>"
## Maya
set AR_DCC_NAME=maya
set MAYA_USD_SDK_ROOT="/path/to/maya/usd/sdk/root/.../mayausd/USD"
set MAYA_USD_SDK_DEVKIT_ROOT="/path/to/maya/usd/sdk/root/.../content/of/devkit.zip"
set PYTHON_ROOT="/path/to/python/root"
## Resolver
set AR_RESOLVER_NAME=fileResolver
```
~~~

## Running the build [开始构建]
To run the build, run:

[ 要运行构建，请运行]

~~~admonish warning title="Houdini GCC ABI Change"
Starting with Houdini 20, SideFX is offering gcc 11 builds that don't use the old Lib C ABI. Our automatic GitHub builds make use of this starting Houdini 20 and upwards.
To make our CMake script still work with H19.5, we automatically switch to use the old ABI, if the Houdini version 19.5 is in the Houdini root folder path.

[ 从Houdini 20开始，SideFX提供了使用 gcc 11 构建的版本，这些版本不再使用旧的 Lib C ABI. 我们的自动 GitHub 构建从 Houdini 20 及更高版本开始采用了这一特性. 为了让我们的 CMake 脚本仍然与 H19.5 兼容，如果 Houdini 的根文件夹路径中包含版本 19.5，我们会自动切换到使用旧的 ABI]

If you want to still build against gcc 9 (with the old Lib C ABI) with Houdini 20 and upwards, you'll need to set `_GLIBCXX_USE_CXX11_ABI=0` as described below and make sure you have the right Houdini build installed.

[ 如果您仍想在 Houdini 20 及更高版本上使用 gcc 9（带有旧的Lib C ABI）进行构建，您需要按照下文的说明设置_GLIBCXX_USE_CXX11_ABI=0，并确保安装了正确的Houdini构建版本]

If you want to enforce it manually, you'll need to update the line below in our main CMakeLists.txt file.
For gcc 9 builds Houdini uses the old Lib C ABI, so you'll need to set it to `_GLIBCXX_USE_CXX11_ABI=0`, for gcc 11 to `_GLIBCXX_USE_CXX11_ABI=1`.

[ 如果您想手动执行此操作，您需要更新我们在主 CMakeLists.txt 文件中的下面这行. 对于使用 gcc 9 构建的 Houdini，它使用的是旧的 Lib C ABI，因此您需要将其设置为 _GLIBCXX_USE_CXX11_ABI=0；而对于使用 gcc 11 构建的，则需要将其设置为 _GLIBCXX_USE_CXX11_ABI=1]

See the official [Release Notes](https://www.sidefx.com/docs/houdini/news/20/platforms.html) for more information.

[ 有关更多信息，请参阅官方[发行说明](https://www.sidefx.com/docs/houdini/news/20/platforms.html)]
```bash
    ...
    add_compile_definitions(_GLIBCXX_USE_CXX11_ABI=0)
    ...
```
~~~

~~~admonish info title=""
```bash
# Linux
./build.sh
# Windows
build.bat
```
~~~

The `build.sh/.bat` files also contain (commented out) the environment definition part above, so alternatively just comment out the lines and you are good to go.

[ build.sh/.bat 文件也包含（被注释掉的）上述环境定义部分，因此，您还可以选择直接注释掉这些行，然后即可进行构建]

## Testing the build [测试构建]
Unit tests are automatically run post-build on Linux using the Houdini/Maya version you are using. You can find each resolvers tests in its respective src/<ResolverName>/testenv folder.

[ 在Linux上，单元测试会在构建后自动运行，使用的是您正在使用的 Houdini/Maya 版本. 您可以在各自的src//\<resolver_name\>/testenv文件夹中找到每个解析器的测试]

Alternatively you can run Houdini/Maya and check if the resolver executes correctly. If you didn't use our convenience script as noted above, you'll have to specify a few environment variables, so that our plugin is correctly detected by USD.

[ 或者，您可以运行 Houdini/Maya 并检查解析器是否执行正确. 如果您没有使用上面提到的我们的便捷脚本，您需要指定几个环境变量，以便 USD 能够正确检测到我们的插件]

Head over to our [Resolvers > Environment Variables](../resolvers/overview.md#environment-variables) section on how to do this.

[ 请前往我们的 [Resolvers > Environment Variables](../resolvers/overview.md#environment-variables) 部分了解如何执行此操作]

After that everything should run smoothly, you can try loading the examples in the "files" directory or work through our [example setup](../resolvers/ExampleSetup/overview.md) section for a simple production example.

[ 之后，一切都应该顺利运行，您可以尝试加载“files”目录中的示例，或者通过我们的示例设置部分来获取简单的生产示例]

## Customize build [自定义构建]
If you want to further configure the build, you can head into the [CMakeLists.txt](https://github.com/LucaScheller/VFX-UsdAssetResolver/blob/main/CMakeLists.txt) in the root of this repo. In the first section of the file, you can configure various things, like the environment variables that the resolvers use, Python module namespaces and what resolvers to compile.
This is a standard `CMakeLists.txt` file that you can also configure via [CMake-GUI](https://cmake.org/cmake/help/latest/manual/cmake-gui.1.html). If you don't want to use the `build.sh` bash script, you can also configure and compile this project like any other C++ project via this file.

[ 如果您想要进一步配置构建过程，可以前往此存储库根目录下的 [CMakeLists.txt](https://github.com/LucaScheller/VFX-UsdAssetResolver/blob/main/CMakeLists.txt) 文件.在文件的第一个部分中，您可以配置各种内容，例如解析器使用的环境变量、Python模块命名空间以及要编译的解析器. 这是一个标准的 CMakeLists.tx t文件，您也可以通过 [CMake-GUI](https://cmake.org/cmake/help/latest/manual/cmake-gui.1.html) 进行配置. 如果您不想使用 build.sh bash 脚本，也可以通过此文件像配置其他 C++ 项目一样配置和编译此项目]

# Documentation [文档]
If you want to locally build this documentation, you'll have to download [mdBook](https://github.com/rust-lang/mdBook) and [mdBook-admonish](https://github.com/tommilligan/mdbook-admonish) and add their parent directories to the `PATH`env variable so that the executables are found.

[ 如果您想在本地构建此文档，则必须下载 [mdBook](https://github.com/rust-lang/mdBook) 和 [mdBook-admonish](https://github.com/tommilligan/mdbook-admonish) 并将其父目录添加到 PATH 环境变量中，以便找到可执行文件]

You can do this via bash (after running `source setup.sh`):

[ 您可以通过 bash 执行此操作（运行 source setup.sh ）]
~~~admonish info title=""
```bash
export MDBOOK_VERSION="0.4.28"
export MDBOOK_ADMONISH_VERSION="1.9.0"
curl -L https://github.com/rust-lang/mdBook/releases/download/v$MDBOOK_VERSION/mdbook-v$MDBOOK_VERSION-x86_64-unknown-linux-gnu.tar.gz | tar xz -C ${REPO_ROOT}/tools
curl -L https://github.com/tommilligan/mdbook-admonish/releases/download/v$MDBOOK_ADMONISH_VERSION/mdbook-admonish-v$MDBOOK_ADMONISH_VERSION-x86_64-unknown-linux-gnu.tar.gz | tar xz -C ${REPO_ROOT}/tools
export PATH=${REPO_ROOT}/tools:$PATH
```
~~~

You then can just run the following to build the documentation in html format:

[ 然后，您可以运行以下命令来构建 html 格式的文档]
~~~admonish info title=""
```bash
./docs.sh
```
~~~

The documentation will then be built in docs/book.

[ 然后，文档将构建在docs/book中]