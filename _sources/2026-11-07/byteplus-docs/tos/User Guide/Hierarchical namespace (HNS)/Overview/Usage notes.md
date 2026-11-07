---
title: "Usage notes"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Usage-instructions"
---

Before using the hierarchical namespace feature, carefully read this document to avoid affecting its normal operation.

<span id="5718447d"></span>
## Prerequisites

For regions currently supporting the hierarchical namespace feature, refer to [Supported regions](https://docs.byteplus.com/docs/tos/What-is-hierarchical-namespace#a9f27159).

<span id="2c938490"></span>
### Using hierarchical metadata

Hierarchical buckets organize metadata according to a new hierarchical structure, thus including directory entities. While supporting the original flat bucket access interfaces, some access behaviors are optimized. Using unsupported access methods for TOS may impact performance and user experience. Pay attention to the following when accessing hierarchical buckets and use the recommended methods.

<span id="1aae7600"></span>
### Recommended methods


1. Use hierarchical listing (with `delimiter` and only the directory separator allowed)`/`), with excellent performance.

2. If you need to hide business details during file writing, create a temporary file, append content, and rename it to the official name after writing.

3. Use object multipart upload to accelerate single\-file concurrent uploads.


<span id="1aae7600"></span>
### Not recommended behavior


1. Flat listing (without `delimiter`) is not recommended.

2. Directories cannot be overwritten; creating an existing directory shows success but does not create a new directory.

3. Hierarchical buckets follow eventual consistency. Renaming parent directories during object upload makes the original file path (object key) inaccessible after upload, requiring reconstructing the object key with the renamed parent directories. This also applies if the parent directory is renamed before the multipart object upload completes.

4. It is not recommended to use third\-party S3\-compatible tools with hierarchical buckets.

   Hierarchical buckets strictly manage metadata in a "hierarchical" way, distinguishing directories and files; flat buckets manage metadata in a "flat" way, treating all as objects. These two management methods cause some differences: there are differences between simulating directory hierarchy using only object keys and having an actual directory hierarchy system, such as deleting directories, listing subdirectories and files, which behave differently in the two types of buckets. Therefore, **using third\-party S3\-compatible tools to connect to hierarchical buckets is not recommended**. For example, Hadoop S3A component may send directory deletion requests that cause conflict errors on the server, leading to business connection failures; tools that mount buckets as local file systems using the S3 protocol may confuse directories and files, causing business failures. If you need to use third\-party S3\-compatible tools, it is recommended to consult technical support first.


<span id="6ea069eb"></span>
## Restrictions


|Category |Constraint |
|---|---|
|Creation count |Each account can create up to 100 hierarchical and flat buckets. |
|Bucket name |Bucket name constraints and limitations, see [Bucket](https://docs.byteplus.com/docs/tos/docs-common-concepts#bucket). |
|Directory name |The delimiter between directories, subdirectories, or files is`/`used as a fixed delimiter and can only be used as the delimiter when listing. |
|Object name |Supports object full paths up to 1024 characters long, with a maximum of 512 directory levels. |
|Per\-bucket limits |* Each bucket has a QPS limit of 300,000. If you need a higher QPS, plan ahead by splitting your workloads across multiple buckets to balance the load.<br><br>* Each bucket can contain up to 500 million directories. To exceed this limit, contact technical support to request an extension.<br><br>* There is no limit to the number of objects that can be stored in a single bucket or directory. However, storing too many objects in a single directory is not recommended, as it may affect the directory's concurrent throughput. |
|EMR Proton version |EMR Proton 2.0 and later versions support hierarchical buckets. If your Proton version is below 2.0, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170) to contact  technical support for a Proton version update. |
