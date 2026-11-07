---
title: "Limits"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Limits"
---

This article describes the usage limitations of file storage PFS.

<span id="文件系统限制"></span>
## File system limitations


|Restrictions |Description |
|---|---|
|The number of file systems that can be created by the same account in the same region |2<br><br>If you need to create more than 2 file systems in the same region,please submit a work order for processing. |
|The number of mounting services that can be created under the same account and in the same region |5 |
|The number of file systems that can be bound to a single mounted service |10 |
|Whether to support subdirectory mounting |No |
|The number of computing nodes that can be mounted on a single file system |2000. If the number of computing nodes you need to mount exceeds 128, please submit a work order for processing. |
|Maximum capacity of a single file system |1PiB<br><br>If you need to create a file system with a capacity exceeding 200TiB,,please submit a work order for processing. |
|Maximum size of a single file |1PiB |
|The maximum number of files or directories in a single file system |The number of files or directories increases with the capacity of the file system. Each TiB of capacity supports approximately 15 million files or directories, and the maximum limit on a single file system is 3 billion. |
|Maximum length of access path |4096 bytes |
|File name length |255 bytes |
|The maximum number of Filesets that can be created by a single file system |10<br><br>If you need to create more than 10 Filesets, please submit a work order for processing. |
