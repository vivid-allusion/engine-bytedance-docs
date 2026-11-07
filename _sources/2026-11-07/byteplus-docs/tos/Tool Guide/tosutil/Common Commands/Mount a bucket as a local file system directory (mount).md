---
title: "Mount a bucket as a local file system directory (mount)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount"
---

You can use the `mount` command to mount a TOS bucket as a local file system directory, and then access it through POSIX\-compliant interfaces.

<span id="6c053e34"></span>
## Notes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">FSX features robust crash recovery capabilities that effectively minimize data loss and service disruption while enhancing system reliability and security. It is highly recommended for mounting buckets. For more information, see <a href="https://docs.byteplus.com/docs/tos/Overview">Overview</a>.</div>


* <div data-tips="true" data-tips-type="tip">Due to differences in how protocols are implemented, some versions of macOS may experience issues with write operations when using the fusermount command.</div>


* This command can only be executed on Linux or macOS systems.

* The `mount` command relies on fusermount to mount buckets. Make sure that fusermount is installed locally before executing the mount command.

* If multiple clients mount the same TOS bucket, you are responsible for coordinating their behavior.


<span id="e8f62d0a"></span>
## Supported operations

Once you have mounted a bucket locally, you can manage its objects via POSIX\-compliant interfaces on the local system. However, since the local system only partially supports POSIX semantics, certain operations are restricted. Specifically:


* Append\-only writes are permitted for files, but in\-place updates are not supported.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">File writes must follow the open\-to\-close principle. You cannot write a file to the TOS server until after you perform a flush operation.   </div>
   

* The following operations are supported: lookup, getattr, setattr, readdir, read, mkdir, rmdir, create, open, write, flush, fsync, release, unlink, rename, and statfs.

* The following operations are not supported: getxattr, setxattr, removexattr, listxatt, readlink, getlk, setlk, setlkw, link, symlink, allocate, lseek, and copyfilerange.


<span id="ab5b4c95"></span>
## Prerequisites

Before using the `mount` command to mount a bucket, make sure you have installed FUSE.

<span id="f763f624"></span>
## Command syntax

```Bash
./tosutil mount tos://bucket[/prefix] mount_point [-sc=xxx] [-fg] [-ro] [-ad] [-adr] [-aow] [-ar] [-ac] [-ao] [-dau] [-dbcbr] [-vchecksum] [-dm=0] [-fm=0] [-uid=0] [-gid=0] [-pprof] [-pport=0] [-bgt=0] [-etmout=0] [-atmout=0] [-ntmout] [-rconcurrency=0] [-wconcurrency=0] [-oconcurrency=0] [-rl=xxx] [-debug] [-dld=xxx] [-rbs=xxx] [-ups=xxx] [-mrbs=xxx] [-mwbs=xxx] [-tfd=xxx] [-futf] [-cctf] [-mts=xxx] [-rlft=1] [-cfd=xxx] [-mcs=0] [-rfdl=0] [-wfdl=0] [-ntfc] [-nftr] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```


<span id="f3b26b59"></span>
## Notes

For descriptions of common optional parameters, see [Global options](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|prefix |String |Object prefix. |
|mount_point |String |The path of the local file system directory where the bucket will be mounted. |
|\-sc |Enum |The storage type of the objects that will be written to the mounted bucket. The options are as follows:<br><br><br>* `STANDARD`: Standard Storage, which is the default value.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive. |
|\-fg |Bool |Mount the bucket as a foreground process. |
|\-ro |Bool |Mount the bucket as a read\-only local file system directory. |
|\-ad |Bool |Allow delete operations on the local file system directory. |
|\-adr |Bool |Allow recursive directory deletion.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>-adr</code> parameter only supports FNS buckets. For more information on FNS buckets, see <a href="https://docs.byteplus.com/docs/tos/Bucket-type">Bucket type</a>.</div><br> |
|\-aow |Bool |Allow overwrite operations on the local file system directory. |
|\-ar |Bool |Allow renaming (moving) operations on the local file system directory. |
|\-ac |Bool |Allow append\-only writes on existing files.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>-ac</code> parameter only supports FNS buckets. For more information on FNS buckets, see <a href="https://docs.byteplus.com/docs/tos/Bucket-type">Bucket type</a>.</div><br> |
|\-ao |Bool |Allow other operating system users to access the local file system directory. |
|\-dau |Bool |Disable automatic unmounting when the process closes. |
|\-dbcbr |Bool |Disable the mechanism that builds a local cache of file metadata through readdir operations. |
|\-vchecksum |Bool |Check data integrity for sequential reads and writes. |
|\-dm |Integer |The permission mode for directories within the local file system. The default value is 0755. |
|\-fm |Integer |The permission mode for files in the local file system. The default value is 0644. |
|\-uid |Integer |The user ID (UID) will be assigned as the owner of the local file system directory. The default is the UID of the current user. |
|\-gid |Integer |The group ID (GID) will be assigned as the owner of the local file system directory. The default is the GID of the current user. |
|\-pprof |Bool |Enable or disable the pprof service. The pprof service is enabled by default. |
|\-pport |Integer |The port number used when enabling the pprof service. The default value is 18888. |
|\-bgt |Integer |The maximum number of asynchronous fuse command requests allowed by the operating system. The default value is 16. |
|\-etmout |Integer |Sets the entry timeout for the local file system directory, in seconds. The default value is 1 second. |
|\-atmout |Integer |Sets the attribute timeout for the local file system directory, in seconds. The default value is 1 second. |
|\-ntmout |Integer |Sets the negative timeout for the local file system directory, in seconds. |
|\-rconcurrency |Integer |The maximum number of concurrent reads from the bucket. The default value is 100,000. |
|\-wconcurrency |Integer |The maximum number of concurrent writes to the bucket. The default value is 100,000. |
|\-oconcurrency |Integer |The maximum concurrency for non\-read/write operations on the bucket. The default value is 1,000. |
|\-rl |Integer/String |The maximum bandwidth (throughput) for read/write operations in bytes. The default value is 1 GB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-debug |Bool |Enable debug logging for the fuse command. |
|\-dld |String |The local directory for debug logs. |
|\-mpt |Integer |The maximum number of prefetch tasks when reading a single file. The default value is 1. |
|\-spt |Integer |The number of shareable prefetch tasks when reading files. If not set, this number is proportional to the maximum bandwidth (throughput) for read/write operations. |
|\-rbs |Integer/String |The cache block size for reading data. The default value is 1 MB, with a maximum of 10 MB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-rps |Integer/String |The maximum part size for reading data. The default value is 8 MB. If not set, the maximum part size depends on the size of the object in the read request.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-ups |Integer/String |The part size for writing data. The default value is 8 MB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-mrbs |Integer/String |The maximum memory available for a single prefetch task when reading an individual object. The default value is 100 MB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-mwbs |Integer/String |The maximum memory available for writing a single object, without using local temporary files. The default value is 50 MB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-mlh |Integer/String |The maximum memory available for read/write operations. This value is set to 70% of the system's total memory by default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>-mlh</code> parameter provides approximate control, rather than precise control, over memory usage. For example, when configured at 50 MB, approximately 50 MB of memory will be available for read/write operations.</div><br> |
|\-tfd |String |The directory for local temporary files, which are used when writing data and when the part size exceeds 20 MB. |
|\-futf |Bool |Force using local temporary files when writing data, regardless of the part size. |
|\-cctf |Bool |Sets whether to calculate the CRC\-64 checksum of the local temporary file when writing data to ensure data integrity during an asynchronous upload. The options are as follows:<br><br><br>* `true` (Default): Calculate the CRC\-64 checksum of the local temporary file when writing data.<br><br>* `false`: Do not calculate the CRC\-64 checksum of the local temporary file when writing data. |
|\-mts |Integer/String |The size limit for the local temporary directory used for writing data. The default value is 1 TB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-rlft |Integer/String |The size limit for large files during rename operations.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-cfd |String |The directory for local cache files used when reading data. If this value is not set, local caching will not be enabled. |
|\-mcs |Integer/String |The maximum space that the local cache can occupy when local caching is enabled. The default value is 1 TB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter supports configuration with capacity units. For example, there is no need to manually calculate how many bytes are in 1 MB—just write "1 MB" and the program will recognize it.</div><br> |
|\-ce |Integer |Sets how long the local cache will be reserved, when local caching is enabled, in seconds. The default value is 3,600 seconds. |
|\-rfdl |Integer |The maximum number of file descriptors that can be open for writing at the same time. The default value is 10,000. |
|\-wfdl |Integer |The maximum number of file descriptors that can be open for reading at the same time. The default value is 10,000. |
|\-nftr |Bool |When a flush operation is performed on an open file descriptor (fd), the data is not written to the bucket immediately, but rather, it is only written upon resource release. |
|\-ntfc |Bool |Sets whether to use the `truncate` parameter when creating a new file. The options are as follows:<br><br><br>* `true`: Do not use the `truncate` parameter when creating a new file.<br><br>* `false` (Default): Use the `truncate` parameter when creating a new file. |


<span id="41e61f71"></span>
## Examples

Use the following command to mount the bucket as a standard local file system directory with overwrite, delete, and move permissions. Example:


* Command


```Plain
./tosutil mount tos://bucket-test mount_path -aow -ad -ar
```



* Output


```Plain
bucket [bucket-test] is mounted at [/root/mount_path] with generation [8282ef44-305f-11ef-a7ae-b645e1163e54]
```



* Check if the bucket is mounted


Use the `df -h <mount_point>` command to check if the bucket is mounted successfully. Example:

```Plain
df -h mount_path
```


If successful, the command returns output containing text similar to the following:

```Plain
Filesystem      Size  Used Avail Use% Mounted on
tosutil/v3.0.1  0.0K  0.0K  0.0K    - /root/mount_path
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To unmount the bucket, use the built\-in command <code>umount <mount_point></code>. Remember not to include the <code>./tosutil</code> prefix when executing this command.</div>
