# File Resolver [文件解析器]
## Overview [概述]
This resolver is a file system based resolver similar to the default resolver with support for custom mapping pairs.

[ 该解析器是基于文件系统的解析器，类似于默认解析器，支持自定义映射键值对]
{{#include ../shared_features.md:resolverSharedFeatures}}
- You can adjust the resolver context content during runtime via exposed Python methods (More info [here](./PythonAPI.md)). Refreshing the stage is also supported, although it might be required to trigger additional reloads in certain DCCs.

    [ 您可以在运行时通过公开的 Python 方法调整解析器上下文内容（更多信息请参见[此处](./PythonAPI.md)）.还支持刷新 stage，尽管可能需要在某些 DCC 中触发额外的重新加载]
- We optionally also support exposing alle path identifiers to our `ResolverContext.ResolveAndCache` Python method. This can be enabled by setting the `AR_CACHEDRESOLVER_ENV_EXPOSE_ABSOLUTE_PATH_IDENTIFIERS` environment variable to `1` or by calling `pxr.Ar.GetUnderlyingResolver().SetExposeAbsolutePathIdentifierState(True)`. This then forwards any path to be run through our mapped pairs mapping, regardless of how the identifier is formatted.

    [ 我们还可以选择支持向 ResolverContext.ResolveAndCache Python 方法公开所有路径标识符. 可以通过将 AR_CACHEDRESOLVER_ENV_EXPOSE_ABSOLUTE_PATH_IDENTIFIERS 环境变量设置为 1 或调用 pxr.Ar.GetUnderlyingResolver().SetExposeAbsolutePathIdentifierState(True) 来启用此功能. 这样，无论标识符的格式如何，都会将所有路径通过我们的映射键值对进行映射处理]

```admonish tip title="Pro Tip"
Optionally you can opt-in into also exposing absolute identifiers (so all (absolute/relative/identifiers that don't start with "/","./","../") identifiers) to our mapping pair mechanism by setting the `AR_FILERESOLVER_ENV_EXPOSE_ABSOLUTE_PATH_IDENTIFIERS` environment variable to `1` or by calling `pxr.Ar.GetUnderlyingResolver().SetExposeAbsolutePathIdentifierState(True)`. This enforces all identifiers to run through our mapped pairs mapping. The mapped result can also be a search path based path, which then uses the search paths to resolve itself. (So mapping from an absolute to search path based path via the mapping pairs is possible.)

[ 您可以选择通过将 AR_FILERESOLVER_ENV_EXPOSE_ABSOLUTE_PATH_IDENTIFIERS 环境变量设置为 1，或者调用 pxr.Ar.GetUnderlyingResolver().SetExposeAbsolutePathIdentifierState(True)，来将绝对标识符（即所有不以 "/", "./", "../" 开头的标识符）暴露给我们的映射机制. 这将强制所有标识符都通过我们的映射键值对进行映射. 映射结果也可以是一个基于搜索路径的路径，然后使用搜索路径来解析自身.（因此通过映射对从绝对路径映射到基于搜索路径的路径是可能的）]
```

{{#include ../shared_features.md:resolverEnvConfiguration}}


## Debug Codes [调试代码]
Adding following tokens to the `TF_DEBUG` env variable will log resolver information about resolution/the context respectively.

[ 将以下标记添加到 TF_DEBUG 环境变量将分别记录有关解析和上下文的解析器信息]
* `FILERESOLVER_RESOLVER`
* `FILERESOLVER_RESOLVER_CONTEXT`

For example to enable it on Linux run the following before executing your program:

[ 例如，要在 Linux 上启用它，请在执行程序之前运行以下命令]

```bash
export TF_DEBUG=FILERESOLVER_RESOLVER_CONTEXT
```