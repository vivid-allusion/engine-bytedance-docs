---
title: "tosfsspec overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_overview"
---

This article mainly introduces the advanced features and best practices of tosfsspec, helping you to fully understand how to use tosfsspec.

<span id="35c9c333"></span>
## Overview

`tosfsspec` is a Python library that follows the [fsspec](https://github.com/fsspec) standard, allowing developers to read and write BytePlus Torch Object Storage (TOS) as conveniently and efficiently as operating a local file system. Whether you are a data analyst or a backend developer, `tosfsspec` provides standard, concise, and feature\-rich interfaces whenever you need to use TOS as the storage backend for Python applications.

You can seamlessly connect to TOS storage capabilities through standard file operation functions like `open()`, `ls()`, `rm()`, easily achieving data upload, download, directory traversal, and management. More importantly, `tosfsspec` deeply integrates with many mainstream data analysis libraries, enabling tosfsspec to read data directly from TOS when processing large datasets without requiring SDK integration or custom wrapping.

<span id="f975acc7"></span>
## **Core features**


* Standardized interface: provides a file system interface fully compatible with `fsspec`, with a low learning curve and easy to use.

* Seamless ecosystem integration: integrates with libraries such as `pandas`, `dask`, and `pyarrow`, configurable via the `storage_options` parameter.

* Extensive file operations: support most file system operations, including reading, writing, appending, copying, moving, deleting, wildcard matching (`glob`), and recursive traversal (`walk`).

* High\-performance IO: built\-in slice upload/download, concurrent task handling, CRC64 checksum, and other mechanisms ensure stable and efficient large\-scale data transfer.

* TOS feature support: supports TOS's HNS (hierarchical namespace) and FNS (flat namespace) bucket types, providing corresponding operation support and usage restrictions.


<span id="4db87f24"></span>
## Differences from s3fs

`s3fs` is a mature library in the `fsspec` ecosystem for interfacing with Amazon S3. tosfsspec inherits its design style but differs in functionality and behavior due to differences in the underlying storage services (TOS vs. S3) and implementation methods.


|**Description** |**s3fs** |**tosfsspec** |**Description** |
|---|---|---|---|
|**Underlying dependencies** |`boto3` / `botocore` |`tosnativeclient` (high\-performance kernel). |`tosfsspec` relies on a self\-developed high\-performance kernel, not the `boto` ecosystem. |
|**Asynchronous support** |Supported (via `aiobotocore`) |No. |`tosfsspec` currently operates entirely in synchronous blocking mode. Calling `await` is not supported in the `asyncio` event loop. |
|**Credential configuration** |Supports multiple methods (environment variables, configuration files `~/.aws/`, IAM Role, explicit input) |Mainly relies on explicitly providing `key`, `secret`, and `region`. |To ensure clarity within the `fsspec` framework, `tosfsspec` recommends explicitly providing credentials during initialization instead of relying on global configuration. |
|**Cache strategy** |Supports multiple `cache_type` options (such as `readahead`, `blockcache`, `simplecache`) |The `cache_type` is fixed to `none`. |`tosfsspec` does not use the cache layer provided by default in `fsspec` but relies on the underlying high\-performance kernel for caching. |
|**Object version control** |Supported (`version_aware=True`) |No. |`tosfsspec` does not support handling multi\-version objects. All operations target the latest version of the object. |
|**Requester Pays** |Supported (`requester_pays=True`) |No. |`tosfsspec` currently does not support the Requester Pays feature. |
|**Server\-Side encryption** |Supported (via `s3_additional_kwargs`) |Partial support (through `storage_class` and others). |TOS uses a different encryption configuration method than S3. `tosfsspec` mainly controls indirectly through the `storage_class` parameter and does not provide a general `s3_additional_kwargs` pass\-through mechanism like `s3fs`. |
|**Multiprocess ** **`fork`** ** safety** |Users must manually set the start method to `spawn` or `forkserver`; otherwise, it is unsafe. |Built\-in `fork` safety mechanism automatically reinitializes the client in child processes. |`tosfsspec` is more robust in `fork` scenarios but using the `spawn` mode is still recommended to fully avoid issues. |
|**HNS/FNS namespaces** |No such concept (S3 uses a flat namespace). |Explicitly supported and handled differently (e.g., restrictions like `maxdepth`). |`tosfsspec` provides compatibility for two bucket types unique to TOS. |


When migrating from `s3fs` to `tosfsspec`, pay attention to the following key points:


* Credential passing: `key`, `secret`, and `region` must be explicitly passed in `storage_options`.

* Parameter cleanup: remove `version_aware`, `requester_pays`, and other `s3fs`\-specific constructor parameters.

* Async refactoring: code involving asynchronous calls must be adjusted to synchronous execution mode.


<span id="fe98e9c9"></span>
## Related documentation

[ ](https://docs.byteplus.com/docs/6349/2275445)

[tosfsspec parameter configuration](https://docs.byteplus.com/docs/6349/2276980)

[tosfsspec path rules](https://docs.byteplus.com/docs/6349/2275446)

[tosfsspec advanced usage](https://docs.byteplus.com/docs/6349/2276979)

[tosfsspec ecosystem integration](https://docs.byteplus.com/docs/6349/2275447)

[tosfsspec performance](https://docs.byteplus.com/docs/6349/2275449)

[tosfsspec troubleshooting](https://docs.byteplus.com/docs/6349/2275448)

[tosfsspec API overview](https://docs.byteplus.com/docs/6349/2276981)
