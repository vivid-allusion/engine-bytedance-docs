---
title: "PyProton introduction and usage documentation"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/PyProton_introduction_and_usage_documentation"
---

<span id="4624cf51"></span>
## PyProton introduction

PyProton is a Proton Python client that implements the [fsspec](https://filesystem-spec.readthedocs.io/en/latest/) standard interface (fsspec is a project designed to provide a unified Python\-style interface for local, remote, and embedded file systems as well as byte storage). PyProton enables Python users to easily access various backend storage systems supported by Proton (such as TOS and HDFS) using familiar methods, while automatically gaining the advantages of Proton storage access (such as stability, performance optimization, and more; for details, please refer to the [Proton official documentation](https://docs.byteplus.com/docs/E-MapReduce/109367)).

<span id="4d34d2b4"></span>
## Prerequisites (checklist)


* JDK 1.8 must be pre\-installed (already included in EMR nodes and Ray images)

* Python 3.9+ must be pre\-installed (as well as a PIP version compatible with Python 3.9+)


<span id="9a21b843"></span>
## Installation


* Built\-in installation: The latest Ray and Spark images have PyProton pre\-installed. For specific version information, refer to the image documentation for [Ray](https://docs.byteplus.com/docs/undefined/69aa39258f7b90052e4c5ea4) and [Spark](https://docs.byteplus.com/docs/E-MapReduce/109078).

* Manual installation:


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Latest package download address: https://proton\-pkgs.tos\-cn\-beijing.volces.com/public/pyproton\-2.1.dev0\-py3\-none\-any.whl.</div>


```Shell
# 可以先通过 pip list 检查是否已预装；
pip list | grep 'pyproton'

# 将下面的包替换为具体的名称；
pip install pyproton-x.whl
```


<span id="ae28895c"></span>
## Usage tutorial

<span id="779d05f0"></span>
### Parameter settings

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are two ways to configure parameters:</div>



* <div data-tips="true" data-tips-type="tip">Via environment variables.</div>


* <div data-tips="true" data-tips-type="tip">Via code\-based initialization settings.</div>



<div data-tips="true" data-tips-type="tip">Environment variables can only set some parameters, while code\-based settings support configuring all parameters. If a parameter is set in both environments, the code\-based setting takes precedence over the environment variable.</div>



1. Environment variables:


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Execute the following commands in sequence, or save them as a script to run.</div>


```Bash
# 替换下文中的bucket name, ak, sk为真实值！

cat > setup-pyproton-env.sh << 'EOF'
#!/usr/bin/env bash
set -exv

# 配置 (ak & sk) 或者 assume role的session token 两者二选一
echo "export TOS_ACCESS_KEY_ID='ak'" >> /etc/profile
echo "export TOS_SECRET_ACCESS_KEY='sk'" >> /etc/profile
echo "export TOS_SESSION_TOKEN='sessiontoken'" >> /etc/profile

# 请注意内外网 end point不同
echo "export TOS_ENDPOINT='http://tos-cn-beijing.volces.com'" >> /etc/profile

# 用于配置pyproton 的log level，如果想调试程序，可以配置为“DEBUG”模式，建议非生产环境下开启
echo "export PROTONFS_LOGGING_LEVEL='INFO'" >> /etc/profile

# 显式覆盖 pyproton 内部Proton SDK的JVM -Xmx参数（默认值为2g）
echo "export PYPROTON_JVM_XMX='4g'" >> /etc/profile
EOF

chmod +x setup-pyproton-env.sh

./setup-pyproton-env.sh

source /etc/profile
```



2. Setting parameters programmatically (all of the above parameters can be set via code):

   * Minimal parameter settings:


```Bash
from pyproton.protonfs import (
    ProtonFileSystem,
    ProtonError,
)
from pyproton.protonfs import ProtonFile
import string
import os

fs = ProtonFileSystem(
    endpoint_url="http://tos-cn-beijing.volces.com",
    key="",
    secret="",
    session_token="",
)
```



* Full parameter settings:


```Bash
from pyproton.protonfs import (
    ProtonFileSystem,
    ProtonError,
)
from pyproton.protonfs import ProtonFile
import string
import os

fs = ProtonFileSystem(
    endpoint_url="http://tos-cn-beijing.volces.com",
    key="",
    secret="",
    session_token="",
    # 用户可按需调整JVM参数，默认的使用无需指定，使用PyProton内置的参数即可
    jvm_args = [
        "-Xms64m",
        "-Xmx2g",
        "-XX:+UseG1GC",
        "-XX:+UnlockExperimentalVMOptions",
        "-XX:MaxGCPauseMillis=100",
        "-XX:G1NewSizePercent=5",
        "-XX:InitiatingHeapOccupancyPercent=65",
        "-XX:+ParallelRefProcEnabled",
        "-XX:ConcGCThreads=4",
        "-XX:ParallelGCThreads=16",
        "-XX:MaxTenuringThreshold=1",
        "-XX:G1HeapRegionSize=32m",
        "-XX:G1MixedGCCountTarget=64",
        "-XX:G1OldCSetRegionThresholdPercent=5",
        "-Dfile.encoding=UTF-8",
        "-Duser.timezone=GMT+08",
        "-XX:+HeapDumpOnOutOfMemoryError",
        "-XX:HeapDumpPath=./java_heapdump.hprof",
    ],
    # proton sdk支持的参数设置
    config_dict = {
        # PROTON_CONFIG_KEY_TOS_ENDPOINT: "http://tos-cn-beijing.volces.com",
        # PROTON_CONFIG_KEY_TOS_AK: "",
        # PROTON_CONFIG_KEY_TOS_SK: "",
        # PROTON_CONFIG_KEY_TOS_SESSION_TOKEN: "",
        "fs.tos.credentials.provider": "io.proton.common.object.tos.auth.DefaultCredentialsProviderChain",  # noqa: E501
        "fs.AbstractFileSystem.tos.impl": "io.proton.fs.ProtonFS",
        "fs.tos.impl": "io.proton.fs.ProtonFileSystem",
        "fs.tos.credential.provider.custom.classes": "io.proton.common.object.tos.auth.EmrSidecarCredentialProvider,io.proton.common.object.tos.auth.EnvironmentCredentialsProvider,io.proton.common.object.tos.auth.SimpleCredentialsProvider,io.proton.common.object.tos.auth.IAMInstanceCredentialsProvider",  # noqa: E501
        # "fs.tos.multipart.staging-dir": "",
        # "fs.tos.multipart.size": "8388608",
        # "fs.tos.multipart.thread-pool-size": "96",
        # "fs.tos.multipart.staging-buffer-size": "4096",
        # "fs.tos.multipart.threshold": "10485760",
        # "fs.tos.task.thread-pool-size": "96",
    }
)
```


When setting parameters programmatically, PyProton is designed for usability and flexibility, which is mainly reflected in two parameters:


* jvm_args: Used to set the JVM parameters required by ProtonSDK. In most cases, users do not need to specify these parameters and can use PyProton's built\-in defaults. If optimization is required, refer to the sample code above to override some default parameters (such as adjusting Xmx).

* config_dict: Used to set parameters required by ProtonSDK. By default, only parameters with the key prefix "PROTON_CONFIG_KEY" need to be set; other parameters use PyProton's built\-in defaults. If optimization is required, refer to the [Proton SDK optimization guide](https://docs.byteplus.com/docs/undefined/69aa39258f7b90052e4c5ea4) and configure as needed.


<span id="b70107fe"></span>
### API invocation

After obtaining the `fs` object, users can call fsspec\-compatible APIs such as `ls`, `mkdir`, and more to operate or access backend storage supported by Proton:

```Bash
fs.mkdir("xxxx")
fs.ls("xxxx")
with fs.open("path", mode="wb") as f:
    f.write("xxx")
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Reuse the fs object as much as possible. A single fs supports access to multiple buckets, so the bucket name must be included in the access path.</div>


* <div data-tips="true" data-tips-type="tip">When performing file read and write operations with PyProton, use the <code>with as</code> statement whenever possible to ensure files are closed promptly.</div>


* <div data-tips="true" data-tips-type="tip">For high\-frequency read and write operations on large files, it is recommended to split them into chunks, and adjust the <code>-Xmx</code> parameter in the JVM parameter set as appropriate.</div>


* <div data-tips="true" data-tips-type="tip">If the compute node has multiple data disks, refer to the Proton official website for tuning parameters related to "multipart" to achieve better write performance. According to multiple rounds of benchmark analysis, PyProton can achieve near\-linear performance improvement as the number of disks increases in multi\-disk write scenarios.</div>


* <div data-tips="true" data-tips-type="tip">LogLevel configuration: By default, logs from both PyProton and the native Proton SDK are combined and output to the console, and both use a unified LogLevel control (the default value is "INFO", which can be controlled using the <code>PROTONFS_LOGGING_LEVEL</code> system environment variable).</div>



<span id="c8d3e0e6"></span>
### API List

The current list of APIs supported by PyProton is as follows:


* FileSystem operation

   * ls

   * info

   * makedir

   * exists

   * isdir

   * isfile

   * glob

   * touch

   * get_file

   * get

   * put_file

   * put

   * rmdir

   * mv (cross\-bucket mv is currently not supported)

   * download

   * walk

   * find

   * du

   * cat_file

   * copy

* File operation

   * seek

   * write

   * read

   * readline

   * readlines

   * info


<span id="1a2885d8"></span>
### Limitations


* Cross\-bucket operations, such as cross\-bucket copy and mv, are currently not supported.

* Random write is not supported.

* Append semantics are currently not supported (support will be added soon).


<span id="fcecc292"></span>
### PyProton on Ray

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information about the PyProton integration version in the Ray image, refer to the <a href="https://docs.byteplus.com/docs/undefined/69aa39258f7b90052e4c5ea4">Ray image documentation</a>.</div>


PyProton can be used on the Ray engine in two ways:


* Used as a pure Python package, for example, it can be used in Ray's map function.

* When used in conjunction with Ray Data, Ray Data currently supports specifying the pyarrow filesystem. By leveraging PyArrow's filesystem conversion handler [pyarrow.fs.FSSpecHandler](https://arrow.apache.org/docs/python/generated/pyarrow.fs.FSSpecHandler.html), PyProton can be adapted to pyarrow.fs through the fsspec interface, enabling direct use of pyproton within Ray Data. The following is an example:


```Python
from pyproton.protonfs import (
    ProtonFileSystem,
    ProtonError,
    PROTON_CONFIG_KEY_TOS_ENDPOINT,
    PROTON_CONFIG_KEY_TOS_AK,
    PROTON_CONFIG_KEY_TOS_SK
)
from pyproton.protonfs import ProtonFile
from pyarrow import fs
from pyarrow._fs import (  # noqa
    PyFileSystem
)
import ray
import random
import string
import os
from jpype import JClass

proton_fs = ProtonFileSystem(
    # ....
)

pyarrow_fs = PyFileSystem(fs.FSSpecHandler(proton_fs))

dt = ray.data.range(100)
dt.show(5)
dt.write_csv(path = "tos://bucket/path", filesystem = pyarrow_fs)
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If ray.init() needs to be called in the code, place it before initializing ProtonFileSystem; otherwise, an error will occur.</div>
