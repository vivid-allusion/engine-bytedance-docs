---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview"
---

This topic provides an overview of FSX to help you quickly understand and use the tool. It includes information on FSX's features, operating environment, constraints and limitations, workflow, and release notes. FSX is a client that enables you to mount a TOS bucket as a local file system on a Linux system. This allows you to directly manage data through file system operations, eliminating the need to adapt to the TOS API. It also streamlines the development process and enhances data operation efficiency.

<span id="a33b26a1"></span>
## Use cases

FSX supports mounting TOS buckets as a local file system on Linux. This approach is ideal for scenarios requiring file system semantics to access bucket data, such as when training model data in AI/machine learning applications that depend on file system operations.

FSX also allows you to configure prefetch and data caching capabilities when mounting buckets, which improves read performance. For more information on usage scenarios and performance optimizations, see [Optimizing FSX performance](https://docs.byteplus.com/docs/tos/Fsx-performance-tuning).

<span id="35e25f20"></span>
## Features


* FSX supports mounting entire buckets or specific bucket directories on Linux systems.

* Once a TOS bucket is mounted on a Linux system, any local operations, such as adding or overwriting objects, will automatically synchronize with the bucket. Similarly, operations performed on the TOS bucket, such as adding or overwriting objects, will automatically synchronize with the local device.

* FSX supports data caching, including read and write caching, which reduces data access latency and improves system performance.

* FSX supports metadata caching, which improves object operation efficiency.


<span id="e82382a8"></span>
## Operating environment

Currently, FSX only works with x86_64/ARM64 architectures, which are limited to the ecs.c3bl instance series. FSX is not yet compatible with Windows or macOS. Supported environments are listed in the following table.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If your environment is not listed, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245">submit a ticket</a> to our support team.</div>


* <div data-tips="true" data-tips-type="default">The operating systems described here are derived from official BytePlus images. Using third\-party images may result in failed installation or inaccessible mount points. If this happens, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245">submit a ticket</a> to our support team.</div>


* Software requirements

   
   |**Architecture** |**Operating system** |**Distribution** |
   |---|---|---|
   |x86_64 |Debian |11 |
   ||CentOS |7 and 8 |
   ||CentOS Stream |8 |
   ||Ubuntu |18.04, 20.04, 22.04, and 24.04 |
   ||veLinux |1.0 and 2.0 |
   ||Rocky |9.1, 9.2, 9.3, 9.4, and 9.5 |
   |ARM64 |Ubuntu |22.04 |
   ||veLinux |1.0 and 2.0 |
   

* Hardware requirements

   FSX uses system storage space to save cache data, log files, and other content. To ensure FSX runs efficiently and stably, we recommend allocating at least 32 GiB of memory and 50 GiB of disk space for the tool. The following provides a detailed explanation of the disk space requirements for the different types of files used by the tool and the recommended directory structure practices.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Do not modify or delete any files in the following directories. Doing so may cause FSX to malfunction.   </div>
   

   
   |**Directory type** |**Description** |**Configuration methods** |
   |---|---|---|
   |Software installation directory |All FSX executables will be stored in the `/opt/fsx` directory, the software installation directory. We recommend allocating at least 1 GiB of disk space for this directory. |It is system\-generated and cannot be modified. |
   |Process log directory |The directory where FSX process log files are stored. The default location is `/opt/tmp/fsx`. The amount of disk space these files occupy depends on the number of active files and concurrent requests in the system. We recommend allocating at least 2 GiB of disk space for this directory. |Use the `persist_dir` mount parameter to specify the directory for storing FSX process log files. |
   |Read cache directory |FSX provides read caching to improve performance in scenarios where specific objects containing small amounts of data are frequently accessed. To optimize the performance of this feature, we **recommend creating a separate partition for the write and read caches**. Specify the storage path and allocate at least 20 GiB of disk space for this directory.<br><br>For more information on read cache, see [Optimizing read cache performance](https://docs.byteplus.com/en/docs/tos/Fsx-performance-tuning?lang=en#dc99714b). |* Use the `read_cache_dir` mount parameter to specify the storage path of the read cache.<br><br>* Use the `max_read_cache_size` mount parameter to specify the maximum disk space that the read cache can occupy. |
   |Write cache directory |By default, FSX writes data to a local temporary directory. The amount of space used depends on the number of concurrent system writes. **We recommend creating a separate partition for the write and read caches**. Specify the storage path and allocate 10 GiB of disk space for this directory.<br><br>For more information on write cache, see [Optimizing write cache performance](https://docs.byteplus.com/en/docs/tos/Fsx-performance-tuning?lang=en#ebcd14ca). |* Use the `temp_dir` mount parameter to specify the storage path of the write cache.<br><br>* Use the `max_temp_capacity` mount parameter to specify the maximum disk space that the write cache can occupy.<br><br>* Use the `part_size` mount parameter to specify the maximum size of a single write cache temporary file. |
   |Runtime log directory |FSX generates runtime logs during operation. By default, these logs are stored in the `/var/log/fsx` directory. We recommend allocating 2 GiB of disk space for this directory. |It is system\-generated and cannot be modified. |
   


<span id="5e984b08"></span>
## Constraints and limitations

<span id="682a376f"></span>
### Read and write restrictions


|Category |Description |
|---|---|
|Access restrictions |* Before they can be accessed, objects in Archive, Cold Archive, and Deep Cold Archive must be restored.<br><br>* Only TOS endpoints are supported when you use FSX to mount a bucket. S3 endpoints are not yet supported. |
|Write restrictions |* Data consistency cannot be guaranteed when multiple clients simultaneously mount the same bucket and write to the same object.<br><br>* Newly created objects are uploaded to TOS only after they are closed. This makes them visible to other clients.<br><br>* The number of `flush` operations permitted after appending data to an object varies depending on the type of object. Specifically:<br><br>   * When appending data to an object in an FNS bucket, TOS uses the `UploadPartCopy` API to copy the existing data, and the `UploadPart` or `PutObject` API to upload the new appended data. In this scenario, one open operation supports only one `flush` operation.<br><br>   * When appending data to an object in an HNS bucket, TOS uses the `AppendObject` API. In this scenario, multiple `flush` operations are supported on appended objects.<br><br>* When overwriting an existing object, you must set the `O_TRUNC` flag to open the object.<br><br>* Large objects are uploaded using the multipart upload method, with a maximum of 10,000 parts per object. The default part size is set at 8 MB. To upload objects larger than 80,000 MB, increase the part size as needed. For more information, check the `part_size` parameter in [Mount parameters](https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description?lang).<br><br>* Renaming objects when mounting an [FNS bucket](https://docs.byteplus.com/en/docs/tos/Bucket-type) may not be an atomic operation. Specifically:<br><br>   * FSX prioritizes using the `RenameObject` API, which is atomic if executed successfully;<br><br>   * If the object does not support `RenameObject`, FSX renames the object using the `CopyObject` and `DeleteObject` APIs. If the `DeleteObject` operation fails, the original object will remain.<br><br>* Concurrent writes to the same object are not supported. If concurrent write requests occur, the first request will succeed, and subsequent requests will fail. |


<span id="beb9b081"></span>
### POSIX compatibility

Once a bucket is mounted on a Linux system, objects can be managed via POSIX\-compatible interfaces. However, since FSX only partially supports POSIX semantics, certain operations are restricted.

The symbols used in the tables are described as follows:​


* ✅: Supported.

* ✔️: Partially supported (see remarks for details).

* ❌: Not supported.



|Category |POSIX interface |Description |Supported or not |Remarks |
|---|---|---|---|---|
|Object attributes |statfs |Returns statistics about a file system. |✅ |None. |
||fstat |Returns attributes of an object. |✅ |None. |
||getattr/setattr |Returns or modifies attributes of an object or directory. |✔️ |Enable the compatible mode when using time\- or permission\-related functions.<br><br>For `chmod`and `chown`:<br><br><br>* We recommend performing these operations after the object is closed.<br><br>* If the `mode` and `own` attributes are not set, the mount parameters (`uid`, `gid`, `file_mode`, and `dir_mode`) are used instead. For descriptions of these parameters, see [Mount parameters](https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description).<br><br>* FSX persists related attributes through the object's user\-defined metadata. By default, FSX queries the corresponding metadata of the folder when `readdir` is called. To improve performance, you can configure the `tos_num_readdir_meta` parameter when mounting. |
||lookup |Looks up an object or directory. |✅ |None. |
|Object writes |flush |Forces a write of buffered data to the output stream. |✅ |None. |
|Directory operations |opendir |Opens a directory stream to read the contents of the directory. |✅ |None. |
||readdirplus |Provides additional information about directory entries. |✅ |None. |
||releasedir |Releases resources associated with a directory stream. |✅ |None. |
||mkdir |Creates a directory. |✅ |None. |
||rmdir |Removes an empty directory. |✅ |None. |
|Basic object operations |create |Creates a folder. |✅ |None. |
||open |Opens an object. |✔️ |Enable the compatible mode when using the `O_TRUNC` flag. |
||close |Closes an open file descriptor. |✅ |None. |
||read |Performs a sequential read. |✅ |None. |
||pread |Performs a random read. |✅ |None. |
||write |Performs a sequential write. |✅ |* Concurrent writes will be serialized.<br><br>* Regardless of whether the `O_APPEND` flag is used, when business software writes to the end of an object, FSX treats it as an append\-only write and processes it accordingly. |
||pwrite |Performs a random write. |✔️ |Enable the compatible mode. |
||release |Releases a file descriptor. |✅ |None. |
||forget |Notifies the file system server to forget the state of an object. |✅ |None. |
||rename (object) |Changes the name of an object. |✅ |Renaming an object or the folder containing it while reading or writing the object is not supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Before renaming an object, first enable the <code>RenameObject</code> feature. For instructions, see <a href="https://docs.byteplus.com/en/docs/tos/Use-renameobject">Enabling RenameObject</a>.</div><br><br><br><div data-tips="true" data-tips-type="default"><code>RenameObject</code> only works for objects uploaded after the feature is enabled. For instructions, see <a href="https://docs.byteplus.com/en/docs/tos/Use-renameobject">Enabling RenameObject</a>.</div><br> |
||rename (directory) |Changes the name of a directory. |✅ |Renaming a directory may not be an atomic operation. |
||unlink |Deletes an object. |✅ |You cannot delete objects while they are being read or written. |
|Object operations |setlk |Sets a lock on an object. |❌ |None. |
||getlk |Checks the lock status of an object. |❌ |None. |
||flock |Applies or removes a lock on an object. |✅ |None. |
||truncate |Truncates an object to a specified size (by path). |✔️ |Enable the compatible mode. |
||ftruncate |Truncates an open object to a specified size (by file descriptor). |✔️ |Enable the compatible mode. |
||utime |Changes the access and modification times of an object. |✔️ |Enable the compatible mode. |
||lseek |Sets the read/write position in an open object. |✅ |None. |
||access |Checks if the calling process has access to an object. |❌ |The kernel automatically checks permissions. |
|Links |Hard link |Uses a hard link. |❌ |None. |
||symlink |Creates a symlink that points to an object. |✅ |If the compatible mode is not enabled: In non\-FSX scenarios, clients accessing a symlink using the TOS protocol cannot resolve a secondary symlink to reach the target object if the symlink points to another symlink. |
||readlink |Reads a symlink. |✅ |None. |
|Extended attributes |setxattr |Sets extended attributes for an object or directory. |❌ |None. |
||getxattr |Returns extended attributes of an object or directory. |❌ |None. |
|Others |mknod |Creates special files in the file system, including character and block devices. |✅ |None. |
||fallocate |Allocates space for an object. |❌ |None. |
||copy_file_range |Efficiently copies object contents within a file system. |❌ |None. |
||poll |Monitors multiple file descriptors for I/O readiness. |❌ |None. |
||bmap |Returns the physical block number of a file on the disk. |❌ |None. |
||ioctl |Performs device‑specific control operations on a file descriptor. |❌ |None. |
||fsync |Synchronizes buffered data with the local disk. |✅ |This interface persists data to the local disk. The data is uploaded to TOS after a flush operation. |


&nbsp;

<span id="1f6e28a4"></span>
## Release notes


|Version number |Release type |Release date |Description |
|---|---|---|---|
|1.4.0.1846 |Latest release |2026\-10\-08 |Optimized stability. |
|1.3.6.1271 |Previous release |2026\-07\-27 |Optimized metadata operations to reduce I/O operations. |
|1.3.4.285 |Previous release |2026\-06\-26 |Fixed a low\-probability issue where the system would hang during reads. |
|1.3.4.282 |Previous release |2026\-06\-16 |* The compatible mode now supports `truncate` by `path`.<br><br>* Fixed a `mount` failure issue caused by excessive concurrency of `opendir`. |
|1.3.2.790 |Previous release |2026\-04\-03 |* A POSIX\-compatible mode is now available. This mode can be enabled using the `compatible_mode=true` mount parameter.<br><br>* Fixed several issues to improve stability. |
|1.3.1.730 |Previous release |2026\-03\-16 |* Enhanced directory detection and compatibility.<br><br>* Optimized support for writing large objects. |
|1.3.1.440 |Previous release |2026\-01\-20 |Optimized support for writing large directories to improve stability. |
|1.3.1.372 |Previous release |2026\-01\-19 |* Optimized the symlink mode.<br><br>* Broadened compatibility for directory permission scenarios.<br><br>* Enhanced data reliability during the write process. |
|1.3.0.855 |Previous release |2025\-12\-26 |Enhanced compatibility for symlinks. |
|1.3.0.370 |Previous release |2025\-12\-04 |FSX now supports Rocky Linux operating systems from version 9.1 to 9.5. |
|1.2.7.546 |Previous release |2025\-11\-24 |Added the `tos_symlink_mode` mount parameter to specify the symlink mode. For more information, see [Mount parameters](https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description). |
|1.2.7.534 |Previous release |2025\-11\-13 |Optimized read cache performance. |
|1.2.7.530 |Previous release |2025\-11\-03 |* FSX now supports ARM64 architecture. For more information, see [Operating environment](https://docs.byteplus.com/en/docs/tos/Overview?lang=en#e82382a8).<br><br>* Enhanced compatibility for symlinks. |
|1.2.6.210 |Previous release |2025\-09\-24 |* Optimized stability.<br><br>* Passwordless mounting of buckets or specified directories via FSX is now available. For more information, see [Passwordless mount](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting?lang=en#14012d4a). |
|1.2.5.520 |Previous release |2025\-09\-03 |Fixed an issue where mounting buckets via HTTPS failed on some operating systems. |
|1.2.5.506 |Previous release |2025\-09\-01 |Optimized stability. |
|1.2.5.331 |Previous release |2025\-08\-15 |FSX now supports configuring server\-side encryption for FNS buckets. However, append\-only writes are not supported. For more information, see [Basic parameters](https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description?lang=en#21be9f9c). |
|1.2.4.386 |Previous release |2025\-07\-31 |Optimized stability. |
|1.2.4.355 |Previous release |2025\-07\-24 |Optimized stability. |
|1.2.3.711 |Previous release |2025\-07\-11 |Optimized stability. |
|1.2.3.592 |Previous release |2025\-07\-04 |Generally available. |
|1.1.0.400 |Previous release |2024\-12\-30 |Initial release. |


&nbsp;

<span id="781da806"></span>
## Workflow


1. [Download and install FSX](https://docs.byteplus.com/en/docs/tos/Install-fsx?lang=en).

2. [Configure FSX and mount a bucket](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting?lang=en).
