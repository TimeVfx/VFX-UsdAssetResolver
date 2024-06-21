
# Python Resolver
## Overview
Python based implemention of the [file resolver](../FileResolver/overview.md):

[ 基于 Python 的 [文件解析器](../FileResolver/overview.md) 实现]
{{#include ../shared_features.md:resolverSharedFeatures}}
- This resolver has feature parity to the file resolver, but the implementation is slightly different. The goal of this resolver is to enable easier RnD by running all resolver and resolver context related methods in Python. It can be used to quickly inspect resolve calls and to setup prototypes of resolvers that can then later be re-written in C++ as it is easier to code database related pipelines in Python.

    [ 该解析器与文件解析器具有相同的功能，但实现略有不同. 该解析器的目标是通过在 Python 中运行所有解析器和解析器上下文相关方法来实现更轻松的 RnD 它可用于快速检查解析调用并设置解析器原型，然后可以用 C++ 重写这些原型，因为用 Python 编写与数据库相关的管道更容易]
- Running in Python does not allow proper multithreading due to Python's [Global Interpreter Lock](https://wiki.python.org/moin/GlobalInterpreterLock), so this resolver should not be used in (large scale) productions.

    [ 由于 [Python 的全局解释器锁](https://wiki.python.org/moin/GlobalInterpreterLock) 在 Python 中运行不允许正确的多线程，因此不应在（大规模）生产中使用此解析器]

{{#include ../shared_features.md:resolverEnvConfiguration}}

## Debug Codes
Adding following tokens to the `TF_DEBUG` env variable will log resolver information about resolution/the context respectively.

[ 将以下标记添加到 TF_DEBUG 环境变量将分别记录有关解析/上下文的解析器信息]
* `PYTHONRESOLVER_RESOLVER`
* `PYTHONRESOLVERR_RESOLVER_CONTEXT`

For example to enable it on Linux run the following before executing your program:

[ 例如要在 Linux 上启用它，请在执行程序之前运行以下命令]

```bash
export TF_DEBUG=PYTHONRESOLVERR_RESOLVER_CONTEXT
```