---
title: "How to handle process exit errors when performing write operations on directories under a Pod"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_handle_process_exit_errors_when_performing_write_operations_on_directories_under_a_Pod"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

When performing write actions on certain directories under the Pod in a **Custom environment command execution** or **Custom steps** task, the pipeline reports the error `cannot create xx/xx: Directory nonexistent`.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The default user for pipeline execution is nobody (uid=65534). The nobody user has very limited privileges and can only write to the `$(CP_WORKSPACE)` directory. If you attempt to write to the `$HOME` directory or any other directory in the Pod for which you do not have permission, errors may occur.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

If you want to perform write operations on directories to which you do not have permission (for example, `/foo`), set the permissions for the corresponding directory to nobody in your Dockerfile in advance.

```dockerfile
FROM ubuntu:latest

...

RUN mkdir -p /foo && chown -R 65534:65534 /foo/

...
```
