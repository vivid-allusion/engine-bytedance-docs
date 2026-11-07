---
title: "Overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_Python_runtime_Overview"
---

This topic describes the runtime environment, development methods, log collection, and Deployment methods for Native Python runtime functions (hereinafter referred to as "Native Python functions").

<span id="runtime-environment"></span>
## Runtime environment

The Native Python runtime supports users in developing Web applications based on the native Python HTTP framework.

<span id="development-language"></span>
## Development language

The Native Python runtime is built\-in with the following versions of Python. There is no need to install a third\-party interpreter when using the following versions.


* Python 3.8

* Python 3.9

* Python 3.12


If you wish to use another version of Python, you can achieve this through the deployment method using [Native runtime](https://docs.byteplus.com/en/docs/faas/Native_runtime) image: import the runtime of the corresponding development language into the Dockerfile, package it with the image, and deploy using the image.

Example: Import the corresponding development language's runtime environment into the Dockerfile.

```dockerfile
FROM python:3
```


<span id="container-environment"></span>
## Container environment

The container environment for Native Python runtime is as follows:


* Operating system version: Debian GNU/Linux 11 (bullseye).

* Architecture: x86_64.


<span id="file-system-restrictions"></span>
## File system restrictions

Only write operations are allowed in the /tmp directory within the container; default temporary storage space is 512 MiB. If the capacity limit is exceeded, the Service will be evicted and restarted.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">User local data written to disk is not persistent; data will be deleted when the container is destroyed, so use with caution. For persistent storage solutions, refer to <a href="https://docs.byteplus.com/en/docs/faas/Function_storage_selection">Function storage selection</a>.</div>
