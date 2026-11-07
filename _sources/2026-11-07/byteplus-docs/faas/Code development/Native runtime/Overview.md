---
title: "Overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_runtime_Overview"
---

Native runtime supports code development based on native HTTP framework. Developing functions with Native runtime requires compliance with Native runtime Specification for Function Service. This topic describes the runtime environment, development methods, log collection, and Deployment methods for Native runtime functions (hereinafter referred to as "Native functions").

<span id="runtime-environment"></span>
## Runtime Environment

Native runtime provides a custom runtime environment offered by the function Service, allowing for the creation of a unique function runtime environment based on Native runtime.


* Customize personalized languages, such as Node.js, Java.

* Customize the runtime environment for specific version of programming languages, such as Node.js 10.


<span id="development-language"></span>
## Development Language

Currently, only the development of Native functions using the Golang language is supported, with more languages to be supported progressively. If you currently wish to use another development language, you can achieve this through the Deployment method using an image: import the runtime of the corresponding development language into the Dockerfile, package it with the image, and deploy the Native functions using the image.

Example: import the runtime environment of the corresponding development language into the Dockerfile.

```dockerfile
# node10
FROM node:10-slim

# java8
FROM java:8-alpine
```


<span id="container-environment"></span>
## Container environment

The container environment for Native runtime is as follows:


* Operating system version: Debian GNU/Linux 11.

* Architecture: x86_64.


<span id="file-system-restrictions"></span>
## File System Restrictions

Only write operations are allowed in the `/tmp` directory within the container; default temporary storage space is 512 MB. If the capacity limit is exceeded, the Service will be evicted and restarted.

tip

User local data written to disk is not persistent; data will be deleted when the container is destroyed, so use with caution. For persistent storage solutions, refer to [Function storage selection](https://docs.byteplus.com/en/docs/faas/Function_storage_selection).
