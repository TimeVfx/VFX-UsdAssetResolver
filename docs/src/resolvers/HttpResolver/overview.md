# Http Resolver (arHttp @charlesfleche)

This is a proof of concept http resolver. This is kindly provided and maintained by @charlesfleche in the [arHttp: Offloads USD asset resolution to an HTTP server
](https://github.com/charlesfleche/arHttp) repository.

[ 这是一个概念验证的 http 解析器. 这是由 @charlesfleche 在 [arHttp:将 USD 资产解析到 HTTP 服务器
](https://github.com/charlesfleche/arHttp) 存储库]

For documentation, feature suggestions and bug reports, please file a ticket there.

[ 如需文档、功能建议和错误报告，请在那里提交票证]

This repo handles the auto-compilation against DCCs and exposing to the automatic installation update manager UI.

[ 此存储库处理针对 DCC 的自动编译并公开给自动安装更新管理器 UI]

## Running the demo server
As the resolver reacts to http requests, we need to setup a local server to answer to our requests.

[ 当解析器对 http 请求作出反应时，我们需要设置一个本地服务器来响应我们的请求]

~~~admonish tip
This can be easily done by running:

[ 这可以通过运行轻松完成]
- <install/dist root folder>/httpResolver/demo/server_install.sh/.bat file to create the python virtual environment with the necessary packages

    [ \<install/dist  root folder\>/httpResolver/demo/server_install.sh/.bat 文件，用于使用必要的包创建 python 虚拟环境]
- <install/dist root folder>/httpResolver/demo/server_launch.sh/.bat file to run the demo server

    [ \<install/dist  root folder\>/httpResolver/demo/server_launch.sh/.bat 文件来运行演示服务器]

Make sure you are running the scripts with the current directory set to <install/dist root folder>/httpResolver/demo, otherwise it won't work!

[ 确保您运行脚本的当前目录设置为 \<install/dist root folder\>/httpResolver/demo 否则它将无法工作！]
~~~

~~~admonish warning
Please make sure that you have python installed at the system level and available on your "PATH" environment variable.
Our install scripts use it to create a virtual environment that runs the http demo server.

[ 请确保您已在系统级别安装了 python 并且在 “PATH” 环境变量中可用. 我们的安装脚本使用它来创建运行 http 演示服务器的虚拟环境]
~~~