---
title: "Introduction and usage of FSSpec"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Introduction_and_usage_of_FSSpec"
---

<span id="2e020f31"></span>
## Introduction

[TOSFS](https://github.com/volcengine/tosfs) is the open\-source implementation of the Proton Python Client. It is built on top of the [Volcano Engine TOS Python SDK](https://github.com/volcengine/ve-tos-python-sdk) and provides a convenient [Python file system interface](https://filesystem-spec.readthedocs.io/en/latest/) for accessing [TOS (object storage)](https://www.volcengine.com/docs/6349/74820).

<span id="4e8d071d"></span>
## Features


* Excellent write performance (optimized through multithreading and multi\-disk caching).

* Robust stability (fine\-grained handling of response codes from the TOS service).

* Outstanding compatibility (cross\-validated across a version matrix of four Python versions and two fsspec versions).

* Native support for TOS features: append API and HNS (Hierarchical Namespace, coming soon).


<span id="2f823657"></span>
## Use cases

TOSFS is suitable for scenarios where object storage operations need to be performed using Python, such as:

**Cloud storage applications**: Developers can build cloud storage applications based on TOSFS to provide online storage, access, and management of files.

**Data processing and analysis**: During data processing and analysis, large amounts of data need to be stored in the cloud and accessed and processed through Python programs. TOSFS provides a convenient file operation interface to help simplify this process.

**Backup and recovery**: TOSFS can be used to easily back up important data and quickly restore it when needed.

<span id="9741c957"></span>
## Installation

You can download TOSFS from the PyPI repository and automatically install it into your Python environment using the following pip command.

```SQL
pip install tosfs
```


<span id="a5de76b2"></span>
## Quick start

<span id="1c3ee7e8"></span>
### Introduction to environment variables


* TOSFS_LOGGING_LEVEL: Used to set the log level for TOSFS (default: WARNING).

* TOS_SDK_LOGGING_LEVEL: Used to set the log level for the tos python sdk dependency of TOSFS (default: WARNING).

* TOS_ACCESS_KEY: Access Key ID, abbreviated as "AK", one of the credentials for accessing TOS.

* TOS_SECRET_KEY: Secret Access Key, abbreviated as "SK", one of the credentials for accessing TOS.

* TOS_SECURITY_TOKEN: Session Token, one of the temporary credentials for accessing TOS. For how to obtain it, refer to the [Assume Role acquisition documentation](https://www.volcengine.com/docs/6723/133859).


<span id="5cf360ba"></span>
### Initialize FileSystem


* Initialize using AK/SK:


```Python
from tosfs.core import TosFileSystem

tosfs = TosFileSystem(
    key='<用户实际的AK>',
    secret='<用户实际的SK>',
    endpoint_url='http://tos-cn-beijing.volces.com', # For intranet usage, replace with the intranet endpoint
    region='cn-beijing',
)
```



* Initialize using system environment variables:


```Shell
# 配置 (ak & sk) 或者 assume role的session token 两者二选一
export TOS_ACCESS_KEY=' <用户实际的AK> '
export TOS_SECRET_KEY=' <用户实际的SK> '
export TOS_SECURITY_TOKEN=' <用户实际的session token> '
export TOS_ENDPOINT='http://tos-cn-beijing.volces.com'
export TOS_REGION='cn-beijing'
```


After confirming that the above environment variables are effective, initialize using `EnvCredentialsProvider`.

```Python
import os
from tosfs.core import TosFileSystem
from tos import EnvCredentialsProvider

tosfs = TosFileSystem(
    endpoint_url=os.environ.get("TOS_ENDPOINT"),
    region=os.environ.get("TOS_REGION"),
    credentials_provider=EnvCredentialsProvider（）, # must
)
```


<span id="eb693211"></span>
### File system and file operation APIs

After obtaining an instance of TosFileSystem as described above, you can access the fs and file operation APIs:

```Python
import os
from tosfs.core import TosFileSystem

# init TosFileSystem
fs = TosFileSystem(
    endpoint_url="https://your-tos-endpoint",
    key="your-access-key",
    secret="your-secret-key",
    region="your-region"
)

local_file_path = "localfile.txt"
remote_file_path = "tos://your-bucket/remote_file.txt"

# create a local file to upload
with open(local_file_path, "w") as f:
    f.write("Hello TOSFS.")

# upload to tos
fs.put_file(local_file_path, remote_file_path)
print(f"Uploaded {local_file_path} to {remote_file_path}")

# download from tos
downloaded_file_path = "downloaded_file.txt"
fs.get_file(remote_file_path, downloaded_file_path)
print(f"Downloaded {remote_file_path} to {downloaded_file_path}")

# read content from downloaded local file
with open(downloaded_file_path, "r") as f:
    content = f.read()
    print(f"Content of {downloaded_file_path}: {content}")

# delete tos file
fs.rm(remote_file_path)

# write to tos
with fs.open(remote_file_path, "w") as f:
    f.write("Hello TOSFS.")

# read from tos
with fs.open(remote_file_path, "r") as f:
    tos_content = f.read()
    print(f"Content of {remote_file_path}: {tos_content}")

# clean local files
os.remove(local_file_path)
os.remove(downloaded_file_path)
```


<span id="f997e104"></span>
## Compatibility

The TOSFS package is compatible with the following Python and fsspec versions.


* Python:



|Version |
|---|
|3.9 |
|3.10 |
|3.11 |
|3.12 |



* fsspec



|Version |
|---|
|2023.5.0 |
|2024.9.0 |


<span id="d2834a3c"></span>
## API documentation

TOSFS provides comprehensive interface documentation. For more information, see [TOSFS Readthedocs API Reference](https://tosfs.readthedocs.io/en/latest/api.html).
