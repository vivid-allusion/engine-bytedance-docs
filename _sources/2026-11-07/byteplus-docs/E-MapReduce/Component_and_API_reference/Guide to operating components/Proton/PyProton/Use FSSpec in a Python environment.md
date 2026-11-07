---
title: "Use FSSpec in a Python environment"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_FSSpec_in_a_Python_environment"
---

TOSFS is a lightweight Python SDK for accessing TOS, allowing users to use it directly in a pure Python environment.

<span id="7d45357f"></span>
## Installation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to use Python version 3.9 or above.</div>


Install the latest version of TOSFS using the following command.

```Shell
pip install tosfs
```


The following example demonstrates how to use common TosFileSystem APIs to read and write TOS.

```Python
import os
from tosfs.core import TosFileSystem

# init TosFileSystem
fs = TosFileSystem(
    endpoint_url="https://{your-tos-endpoint}",
    key="{your-access-key}",
    secret="{your-secret-key}",
    region="{your-region}"
)

local_file_path = "localfile.txt"
remote_file_path = "tos://{your-bucket}/remote_file.txt"

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


When using the above code, replace the `endpoint_url`, `key`, `secret`, and `region` variables with actual authentication information. Also, replace the local path and the path on TOS with valid, real paths to ensure successful execution.
