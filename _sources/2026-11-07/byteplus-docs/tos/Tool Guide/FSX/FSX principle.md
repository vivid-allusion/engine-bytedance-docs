---
title: "FSX principle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Fsx-principle"
---

This article introduces the semantics of FSX client file reading and writing, files, directories, and data caching to help you better use the FSX client.

<span id="08256ef3"></span>
## File reading and writing

Applications can access the entire object or read a specific portion of data at a specified offset within a TOS bucket through the FSX client. The FSX client optimizes for large file sequential read scenarios by automatically prefetching data concurrently from TOS to enhance sequential read throughput. By default, the FSX client does not download files to the local directory or occupy local storage; it only caches data in the read cache directory when the read cache mount parameter is configured.

For write operations, applications must write from the start of the file and support only sequential writes, not random writes. The FSX client writes first to a local temporary file directory by default. The temporary directory can be configured using the `temp_dir` parameter during mounting, and by default, a temporary directory is created under `/tmp/` as the temporary file directory. If you are sensitive to performance, you can specify `tmpfs` as the temporary file directory for writing during mounting. After writing a full part size (part_size), FSX asynchronously uploads this data segment to the TOS server and optimizes write throughput via concurrent uploads.

A file becomes visible to other clients only after the application closes it, and no further writes are allowed on this file. For overwriting an existing file, the application must set the O_TRUNC flag when opening the file, indicating the file needs to be truncated.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since write operations first write data to a temporary file directory, the directory must have enough space to temporarily store the data. The temporary file directory must have at least 10240 times the segment data size available; for the default segment size of 8M, this means 80 GiB of space is required.</div>


<span id="64b65367"></span>
## List files/directories

The FSX client optimizes file/directory listing by adding a prefetch cache to reduce the number of List requests to the TOS server, improving listing performance and lowering List request costs due to the lengthy List operation.

<span id="51666903"></span>
## Files and directories

Directories are crucial to the file system; the FSX client interprets "/" in object names as directory separators to automatically infer the directory structure of the TOS bucket. For example, if the bucket contains an object named dir1/dir2/file, dir1/ and dir2/ are interpreted as directories, and file as a file, forming the file system structure dir1/, dir1/dir2/, dir1/dir2/file.

When directories and files share the same name, the directory takes precedence, and the file is ignored. For example, if both objects a/b and a/b/c exist at the same time, b will be interpreted as a file in a/b and as a directory in a/b/c, so object a/b will be ignored during mapping. If a/b/c is deleted later and there is no naming conflict with b, a/b will become visible again.

<span id="982259ed"></span>
## Data cache

The FSX client supports local data caching, suitable for scenarios involving frequent reads of a small batch of files. By enabling data cache, reading the same batch of data from the same computing instance effectively reduces requests to TOS, lowering costs while improving read performance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Using data cache affects data consistency and validity and may read outdated data. It is not recommended for scenarios requiring high data timeliness and consistency.</div>


<div data-tips="true" data-tips-type="warning">For one\-time file reading scenarios, data cache does not improve performance or reduce costs, so enabling it is not recommended.</div>


After enabling data cache, you need to specify the cache directory and cache size. The FSX client creates a new subdirectory in the specified cache directory during mounting and deletes any files and directories in that subdirectory during mounting and unmounting. When the cached data reaches the set cache size, the FSX client proactively clears the least recently used data blocks from the cache directory.
