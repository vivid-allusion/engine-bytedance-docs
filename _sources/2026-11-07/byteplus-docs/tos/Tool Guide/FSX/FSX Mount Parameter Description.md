---
title: "FSX Mount Parameter Description"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description"
---

This article provides a detailed introduction to the mount parameters that can be configured when using the FSX client, specifically including basic parameters, read cache parameters, write cache parameters, etc.

<span id="21be9f9c"></span>
## Basic Parameters


|**Parameter** |**Is it mandatory** |**Description** |
|---|---|---|
|region |Yes |Region where the bucket is located. |
|no_writeback_cache |Yes |Do not enable the kernel page cache write\-back feature to ensure that write requests are performed sequentially. |
|endpoint |Yes |Access domains for TOS only support TOS domains; S3 domains are not supported at this time. If no protocol is specified, the HTTPS protocol is used by default, and the complete format is `https://{host}:{port}`. |
|access_key_id |No |Specify the key information in the mount command. For detailed instructions on obtaining the Access Key ID and Secret Access Key, please refer to [Access Key (Key) Management](https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Please ensure that the account associated with the Access Key ID and Secret Access Key has read and write permissions for the storage bucket. If the permissions are insufficient, the mount point may become unavailable.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Specifying key information in the mount command and specifying the file path containing authentication information in the mount command are mutually exclusive options; you must configure one of them.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When only temporary access credentials are used, you need to set the <code>security_token</code> parameter.</div><br> |
|secret_access_key |||
|security_token |||
|credential_filepath |No |Specify the absolute path of the authentication credential file to load the authentication information required for access. You need to create the authentication credential file yourself, and the file extension must be `json`, containing the following content:<br><br>```Bash```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
|credential_timeout_sec |No |Validity period of the FSX client dynamic configuration authentication file, in seconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>credential_timeout_sec</code> and <code>credential_filepath</code> parameters must be used together.</div><br> |
|num_meta_threads |No |Metadata thread count, default is 32; it is recommended not to set it below the default value. |
|num_io_threads |No |Number of read threads; the default is 16, and it is recommended not to set it below the default value. |
|num_write_threads |No |Number of write threads: When `num_write_threads` is not specified, the system automatically sets its default value to the value of `num_io_threads`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only FSX tool versions 1.2.7.530 and above support the <code>num_write_threads</code> parameter.</div><br> |
|storage_class |No |Specify the storage type for files uploaded to TOS. Optional parameters are:<br><br><br>* `STANDARD`: Standard Storage, default value.<br><br>* `IA`: Infrequent Access Storage<br><br>* `ARCHIVE_FR`:  Flashback Archive. |
|enable_verify_ssl |No |Configure whether to enable SSL certificate verification. It is enabled by default. The value options are explained as follows:<br><br><br>* `true`: Enable SSL certificate verification.<br><br>* `false`: SSL certificate verification is not enabled. |
|max_inode_num |No |The maximum number of inodes for the current mount point is 10 million by default; The maximum value is 18446744073709551615.it is generally not recommended to modify this value. If the total number of files and directories under the mount point exceeds 10 million, it is recommended to increase this value according to the actual usage. |
|max_file_num |No |The current mount point supports a certain number of handles that can be opened simultaneously; typically, the operating system first restricts the number of file handles a user can open. When operating system restrictions are lifted, it is also necessary to pay attention to whether the value of this parameter is sufficient. The default value of the parameter is 65535. Increasing this parameter value will raise the memory usage of TOS FSx. By default, approximately 50MB of memory is allocated for issuing handles. When the parameter is increased, memory usage grows linearly with the parameter value. |
|rw |No |Mount the file system in read\-write mode; enabled by default. |
|ro |No |Mount the file system in read\-only mode; this is disabled by default and can be enabled by specifying the mount option `-o ro`. |
|max_retry_count |No |Maximum number of retries for failed requests; default is 3. |
|connection_timeout |No |Set the connection establishment timeout period (in milliseconds); the default is 10,000 milliseconds. |
|socket_timeout |No |Request timeout period: if no data is received within the timeout period, the connection will be closed. The default request timeout is 30,000 milliseconds. |
|persist_dir |No |The directory for storing status files during system operation, with the default value set to `/opt/tmp/fsx`. The space occupied by this directory is related to the values of the `max_inode_num` and `max_file_num` parameters. It is recommended to reserve 2GiB of disk space. |
|tos_is_custom_domain |No |Indicates whether the current domain name is a custom domain; the default value is false. |
|tos_incremental_upload |No |Whether to enable append write; the default is false. |
|tos_allow_delete |No |Whether file deletion is permitted; the default value is false. |
|tos_create_empty_file |No |In the scenario of creating a new file, whether to create a 0\-byte file in the TOS bucket during the open operation to ensure visibility; the default is true. |
|tos_sse |No |Set the encryption method for the target object. After mounting is completed, uploaded objects will, by default, use this server\-side encryption method. The value descriptions are as follows:<br><br><br>* `AES256`: Uses the SSE\-TOS encryption method and adopts the AES256 encryption algorithm.<br><br>* `kms`: Uses SSE\-KMS encryption method and applies the AES256 encryption algorithm.<br><br><br>For detailed information on the SSE\-TOS and SSE\-KMS encryption methods, please refer to [Encryption Methods](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview#.5Yqg5a-G5pa55byP).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When using SSE\-TOS or SSE\-KMS for server\-side encryption, the SM4 encryption algorithm is currently not supported.</div><br> |
|tos_sse_kms_key_id |No |The TRN of the KMS master key, used to specify the master key for SSE\-KMS encryption of the target object. The format is `trn:kms:<region>:<accountID>:keyrings/<keyring>/keys/<key>`, where `region` is the Region ID to which the key belongs, `accountID` is the ID of the account to which the key belongs, `keyring` is the keyring alias, and `key` is the master key alias.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can log in to the <a href="https://console.byteplus.com/kms/region:kms+cn-beijing/primary?">KMS Console</a>. On the <strong>Customer Master Key</strong> page, click the target key ring. On the <strong>Key Ring Details</strong> page, locate the <strong>Key TRN and Alias</strong> column of the target key to obtain the key TRN.</div><br> |
|tos_symlink_mode |No |The symlink mode. The values are explained below.<br><br><br>* 0: This mode preserves the original symlink behavior. The system cannot resolve the target object path for symlinks created via the TOS console. For more details, see [Recommendations for accessing symlinks in Linux](https://docs.byteplus.com/docs/tos/Recommendations-for-accessing-symlinks-in-linux).<br><br>* 1: This is a compatibility mode in which the system automatically recognizes server\-side symlinks created via the TOS console. When accessing these symlinks, the system redirects to the content of the target object.<br><br><br>The default value for the `tos_symlink_mode` parameter is 0. |


<span id="d51bd2de"></span>
## Prefetch Parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can set prefetch parameters when mounting a bucket. You can also configure prefetch performance. For a detailed introduction to prefetch performance, please refer to <a href="https://docs.byteplus.com/docs/tos/Fsx-performance-tuning#65d6bdc6">Prefetch Performance</a>.</div>



|**Parameter** |**Is it mandatory** |**Description** |
|---|---|---|
|prefetch_buffer_size |No |The default size of the pre\-read data block is 4 MB (megabytes). |
|prefetch_cache_pool_limit |No |The maximum space occupied by the prefetch cache memory is 1024 MB by default, with the unit being MB. |
|prefetch_forward_buffer_count |No |The maximum number of data blocks that can be pre\-read for a single file is 32 by default. |
|prefetch_backward_buffer_count |No |Retain the number of data blocks preceding the current read request offset; the default value is 1. |
|num_prefetch_threads |No |Number of prefetch threads; the default is 32, and it is recommended not to set it below the default value. |


<span id="84bc309b"></span>
## Read Cache Parameter


|**Parameter** |**Is it mandatory** |**Description** |
|---|---|---|
|read_cache_dir |No |Read cache directory; the default is empty, i.e., the read cache is not used.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to use the read cache function, it is recommended to configure a dedicated data disk or a file system with a separate partition for the read cache, in order to avoid competition for disk space with other system applications. You can configure the same file system partition for both the read cache and the write cache; simply distinguish them by using different directories. If the read cache and write cache share a single partition, it is recommended to reserve a total of 120 GiB of disk space for both the read cache and write cache.</div><br> |
|max_read_cache_size |No |The maximum space occupied by the read cache, measured in MB. The default value is 0, which means that read caching is not used. |


<span id="1ef93285"></span>
## Write Cache Parameter

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Write cache is enabled by default and cannot be disabled. When mounting a bucket, you can set write cache parameters and configure write performance. For a detailed introduction to write performance, please refer to <a href="https://docs.byteplus.com/docs/tos/Fsx-performance-tuning#ebcd14ca">Write Cache Performance</a>.</div>



|**Parameter** |**Is it mandatory** |**Description** |
|---|---|---|
|temp_dir |No |Write cache directory; the default is `/tmp`.<br><br>By default, the FSX client first writes data to a local temporary file directory, which is created under `/tmp/`. You can configure the temporary file directory by specifying the `temp_dir` parameter during mounting. If performance is important to you, you can specify `tmpfs` as the directory for writing temporary files when mounting. For a detailed introduction to write performance, please refer to [Write Cache Performance](https://docs.byteplus.com/docs/tos/Fsx-performance-tuning#ebcd14ca).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to use the write cache function, it is recommended to configure a dedicated data disk or a file system with a separate partition for the write cache, in order to avoid competition for disk space with other applications in the system. You can configure the same file system partition for both the read cache and the write cache, as long as you use different directories to distinguish them. A minimum of 80 GiB of disk space is required for the write cache. If the read cache and write cache share a single partition, it is recommended to reserve a total of 120 GiB of disk space for both the read cache and write cache.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The maximum space occupied by the write buffer is the product of <code>max_temp_parts</code> and <code>part_size</code>. Therefore, the available storage space in the temp_dir directory must be greater than the product of <code>max_temp_parts</code> and <code>part_size</code>; otherwise, mounting the bucket using FSX will fail.</div><br> |
|num_bg_threads |No |The number of threads for uploading multiple segments of data is set to 32 by default; it is recommended not to set this value below the default. |
|part_size |No |The chunk size for multipart uploads is measured in MiB, with a default value of 8 MiB and a valid range of [4, 5120]. TOS restricts the maximum number of segments that can be uploaded to 10,000. The size of the uploaded object can be adjusted by modifying the segment size. For specific usage instructions, please refer to [Uploading Large Files](https://docs.byteplus.com/docs/tos/Upload-large-files).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The value of <code>part_size</code> must be a positive integer.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In scenarios involving a high volume of concurrent uploads, TOS limits the number of objects that can be open in write\-only or read\-write mode concurrently (referred to as 'Limit'), in order to prevent the amount of disk space used by the write cache from exceeding the maximum capacity (max_temp_capacity). The calculation formula is: Limit = max_temp_capacity / part_size. Therefore, increasing the part_size causes the limit value to decrease. In such cases, we recommend increasing the max_temp_capacity value simultaneously.</div><br> |
|max_temp_capacity |No |The maximum disk space occupied by the write cache is measured in GiB, with a default value of 10 GiB. It is recommended not to set this value below the default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only FSX tool versions 1.2.7.530 and above support the <code>max_temp_capacity</code> parameter.</div><br> |


<span id="3725ab72"></span>
## Access Permissions


|**Parameter** |**Is it required** |**Description** |
|---|---|---|
|uid |No |When assigning a file or directory to a specific user, you must enter the user's uid. |
|gid |No |When assigning a file or directory to a user group, you need to provide the group's gid. |
|file_mode |No |Used to set the permissions of mounted files; the default value is 644. |
|dir_mode |No |Used to set directory permissions; the default value is 755. |


<span id="f0b7879b"></span>
## Mounting Method


|**Parameter** |**Is it mandatory** |**Description** |
|---|---|---|
|native_fuse |No |Whether to use the native Linux Fuse tool to mount TOS. Explanation of possible values is as follows:<br><br><br>* `true`: Use the native Linux Fuse tool to mount TOS.<br><br>* `false`: Use FSX tools to mount TOS.<br><br><br>The default is false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After mounting TOS using the native Fuse tool in Linux, please note the following points:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Lossless upgrade is not supported; after upgrading the client, business operations cannot be automatically restored. You need to remount and then manually restore the related business operations.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Automatic cleanup of temporary files is not supported; that is, after restarting the process, temporary files in the write cache directory <code>temp_dir</code> will not be automatically deleted. To prevent disk space from being occupied, you need to manually clean up temporary files on a regular basis.</div><br> |
