---
title: "Overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Python_runtime_Overview"
---

When using the Python runtime to develop functions in Function Service (FaaS), it is necessary to comply with the Python runtime specifications of BytePlus.

This topic describes the runtime environment, development methods, log collection, and packaging methods for Python runtime functions (hereinafter referred to as "Python functions").

<span id="runtime-environment"></span>
## Runtime environment

The current Python runtime versions supported by the Function Service are as follows. You can select the desired runtime environment when creating a function.


* Python 3.8

* Python 3.9

* Python 3.12


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you wish to use another version of Python, you can achieve this through the Deployment method using <a href="https://docs.byteplus.com/en/docs/faas/Native_runtime">Native runtime</a> image: import the runtime of the corresponding development language into the Dockerfile, package it with the image, and deploy using the image.</div>


<span id="file-system-restrictions"></span>
## File system restrictions

Only write operations are allowed in the /tmp directory within the container; default temporary storage space is 512 MiB. If the capacity limit is exceeded, the Service will be evicted and restarted.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">User local data written to disk is not persistent; data will be deleted when the container is destroyed, so use with caution. For persistent storage solutions, refer to <a href="https://docs.byteplus.com/en/docs/faas/Function_storage_selection">Function storage selection</a>.</div>
