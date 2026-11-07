---
title: "FSX troubleshooting and resolution"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Faq"
---

This topic provides guidance on how to troubleshoot and resolve issues that may arise while using FSX.

<span id="861c0ff9"></span>
## Permissions

<span id="4735dfeb"></span>
### Error: "Auth Failed" during mounting

What it means:

The access key ID and secret access key that you used to mount the bucket are either incorrect or do not have the necessary permissions.

How to fix it:


* Verify that the access key ID and secret access key entered during mounting are correct.

* Make sure the account associated with the access key ID and secret access key used for mounting has the minimum required permissions to mount the bucket. For more information, see [Permissions required to mount a bucket](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting).


<span id="d6c3268a"></span>
### Error: “Permission denied” when attempting to read objects after successfully mounting the bucket

What it means:


* The objects are stored in Archive, Cold Archive, or Deep Cold Archive and you did not restore them before reading.

* The access key ID and secret access key that you used to mount the bucket do not have the necessary permissions.


How to fix it:


* If the objects you want to access are stored in Archive, Cold Archive, or Deep Cold Archive, restore them before reading.

* Make sure the account associated with the access key ID and secret access key used for mounting has the GetObject permission. For more information, see [Permissions required to mount a bucket](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting).


<span id="f76f319f"></span>
## Mounting

<span id="38e5f6a2"></span>
### Error: "Mount target directory is not exist" during mounting

What it means:

You did not create the mount directory before mounting the bucket.

How to fix it:

Create a mount directory before mounting. For instructions, see [Configuration and mounting](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting).

<span id="a5ca0ebd"></span>
### Issue: After mounting the bucket with FSX, rebooting the Linux system with `reboot -t` leads to a hang

What it means:

The reboot process was initiated without first unmounting the mount point. In this case, the reboot command terminates all user processes (including FSX) before running the umount command. Since FSX supports crash recovery, the umount operation does not fail immediately. Instead, it waits for FSX to recover, causing the reboot command to hang.

How to fix it:

Force restart the system, or wait for FSX to complete recovery. The system will automatically resume rebooting.

<span id="94cff10a"></span>
### Issue: Failed to mount a bucket or access its objects

What it means:


* The bucket either does not exist or the name is incorrect.

* An S3 endpoint was used when mounting or accessing the bucket.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">FSX only supports TOS endpoints.   </div>
   

* There are either network connectivity issues between the client and TOS, or there are network anomalies.

* The provided credentials are incorrect or the permissions are insufficient when mounting the bucket as an IAM user.


How to fix it:


* Log in to the TOS console or use an API to check if the bucket exists and if the name is correct.

* Make sure you are using a TOS endpoint and not an S3 endpoint. Then, test network connectivity using the following commands:


```Shell
ping tos-cn-beijing.ivolces.com
ping bucket.tos-cn-beijing.ivolces.com
```


For more information on TOS endpoints, see [Regions and endpoints](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint?lang=zh).


* Check the local network's connectivity, DNS resolution, and firewall rules to ensure normal access to TOS endpoints.

* Verify that the access key ID, secret access key, Security Token Service (STS) token, and any other credentials used for mounting are correct. Ensure that the corresponding IAM user has the necessary permissions to mount and access the bucket. For more information on permissions, see [Configuration and mounting](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting).


<span id="2a7b6bb3"></span>
### Issue: Failed to execute the mount command

What it means:


* The mount parameters contain invalid or unsupported parameters.

* The credential file used for the `credential_filepath` parameter is not in the correct JSON format.

* There is insufficient system disk space to run FSX.


How to fix it:


* Check the parameters of the mount command. Make sure that all of the parameters are correct and remove any invalid ones. If you are using an older version, upgrade FSX to the latest version and retry the mount.

* If you are using the `credential_filepath` parameter in the command, make sure the credential file is in valid JSON format. The credential file can be in either of the following formats:


```JSON
{
    "VOLC_ACCESSKEY": "<ak_string>",
    "VOLC_SECRETKEY": "<sk_string>",
    "VOLC_SECURITY_TOKEN": "<sts_string>"
}

or 

{
    "VOLC_ACCESSKEY": "<ak_string>",
    "VOLC_SECRETKEY": "<sk_string>"
}
```



* Make sure there is enough disk space available. We recommend allocating at least 32 GiB of memory and 50 GiB of disk space for FSX. The recommended directory structure practices are listed below.



|Directory type |Description |Configuration methods |
|---|---|---|
|Software installation directory |Default path: `/opt/fsx`. Recommended disk space: ≥ 1 GiB. |It is system\-generated and cannot be modified. For more information, see [Downloading and installing FSX](https://docs.byteplus.com/docs/tos/Install-fsx). |
|Process log directory |Default path: `/opt/tmp/fsx`. Recommended disk space: ≥ 2 GiB. |Use the `persist_dir` parameter to specify the directory for storing FSX process log files. For more information, see [Mount parameters](https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description). |
|Read cache directory |Read caching is disabled by default. The read cache directory is empty. We recommend creating a separate partition and allocating at least 20 GiB of disk space for this directory when read caching is enabled. |Use the `read_cache_dir` parameter to specify the directory for the read cache. Use the `max_read_cache_size` parameter to specify the maximum disk space that the read cache can occupy. For more information, see [Mount parameters](https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description). |
|Write cache directory |Default path: `/tmp`. Recommended disk space: ≥ 10 GiB. We recommend creating a separate partition for the write and read caches. |Use the `temp_dir` parameter to specify the directory for the write cache. Use the `max_temp_capacity` parameter to specify the maximum disk space that the write cache can occupy. Use the `part_size` parameter to specify the maximum size of a single write cache temporary file. For more information, see [Mount parameters](https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description). |
|Runtime log directory |Default path: `/var/log/fsx`. Recommended disk space: ≥ 2 GiB. |It is system\-generated and cannot be modified. For more information, see [Configuration and mounting](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting). |


<span id="53848448"></span>
## Installation

<span id="7aa62940"></span>
### Error: "Package ca\-certificates is not installed" during installation

What it means:


* Your operating environment — including your system architecture, operating system, and distribution — is incompatible with FSX.

* The dependency components are either not installed, or the installed versions are not the required ones.


How to fix it:


1. Check if your operating environment is supported. Currently, FSX only works with x86_64/ARM64 architectures, which are limited to the ecs.c3bl instance series. FSX is not yet compatible with Windows or macOS. See the table below for a list of supported environments.

   
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
   

2. Install the dependencies, and then try installing FSX again.

   ```Shell
   apt update
   apt install ca-certificates
   ```
   


<span id="7b301cf3"></span>
### Issue: Failed to upgrade FSX

What it means:


* Rolling back from a higher version to a lower one can cause upgrade anomalies.

* Other sporadic upgrade failures.


How to fix it:


* If you are downgrading, we recommend first uninstalling the current version and then installing the target version.

* Then, try upgrading FSX again.

* If it still fails after multiple attempts, collect the relevant logs and [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) to us.


<span id="d1cab568"></span>
## Unmounting and uninstallation

<span id="2e03cdeb"></span>
### Error: "target is busy" during unmounting

What it means:

Unmounting will fail if there are still active processes accessing the mount directory.

How to fix it:

Follow these steps to resolve the issue, using `/mnt/point` as an example mount directory.


1. Identify the processes using the `lsof | grep "/mnt/point"` command.

2. Force close the processes accessing the mount directory.

3. Try unmounting again using the `umount /mnt/point` command.


<span id="bbc1d11e"></span>
### Issue: Failed to uninstall FSX

What it means:

Mount points still exist and are considered in use by the system.

How to fix it:


1. Use the `df -h` command to check if any FSX mount points still exist.

2. Run the `umount` command on all mount points. After confirming that no mount points remain, try unmounting again.


<span id="d016028d"></span>
### Issue: Failed to execute the `umount` command.

What it means:

The mount point you want to unmount is occupied by processes accessing it during the unmounting process.

How to fix it:

Using `/mnt/point` as an example mount directory, identify the processes with the following command:

```Shell
lsof | grep "/mnt/point"
```



* Force close or gracefully terminate the processes accessing the mount directory.

* Try unmounting again using the `umount /mnt/point` command.


<span id="efc92175"></span>
## Read and write

<span id="e016f355"></span>
### Issue: Why does copying occur when appending data to objects in an FNS bucket?

What it means:

The way FSX implements append\-only writes differs depending on the bucket type. Specifically:


* When appending data to an object in an FNS bucket, TOS uses the UploadPartCopy API to copy the existing data, and the UploadPart or PutObject API to upload the new appended data. In this scenario, one open operation supports only one flush operation.

* When appending data to an object in an HNS bucket, TOS uses the AppendObject API. In this scenario, multiple flush operations are supported on appended objects.


How to fix it:

To avoid multiplied requests, use an HNS bucket.

<span id="52ac29ce"></span>
### Issue: Failed to access a directory after mounting the bucket

What it means:

Once a bucket is mounted via FSX, the system recognizes objects ending in `/` as directories. If you create a directory and an object with the same name, such as "test/" and "test", the system cannot distinguish between them. This causes directory access to fail.

How to fix it:

We recommend renaming any directories and/or objects with identical names in the mounted bucket to ensure they have unique names. To prevent future naming conflicts, please avoid creating directories and objects with the same name.

<span id="fb68ec71"></span>
### Issue: Failed to read from the mount directory

What it means:


* The system cannot resolve the path correctly when an object and a directory share the same name at any level of the access path, leading to access failures.

   If accessing `A/B/C/1.txt` fails, check if `A`, `A/B`, or `A/B/C` were created as objects along the path. If so, rename these objects to avoid conflicts with directories of the identical names.

* The object is stored in one of the following storage types: Archive, Cold Archive, or Deep Cold Archive. The data has not yet been restored and cannot be read directly.


How to fix it:


* Check each level of the access path for duplicate object and directory names. If there are any, rename the conflicting objects to avoid having identical names with directories.

* Restore the archived data before reading it.


<span id="7feaaa3b"></span>
### Issue: Failed to write to the mount directory

What it means:


* The object you want to write to the directory is either too large, or it does not comply with the recommended writing methods.

* Concurrent writing to the same object may cause the first request to succeed and subsequent requests to fail.

* Opening an object that is currently being read or written with the `O_TRUNC` flag may cause conflicts.

* Overwriting an existing object with an offset of 0 can cause FSX to block the write operation.


How to fix it:


* See [Uploading large objects](https://docs.byteplus.com/en/docs/tos/Upload-large-files?lang=zh) for troubleshooting and optimizing write methods for large objects.

* Avoid writing to the same object at the same time. If necessary, use serialization or locking controls in the application.

* Do not open objects with `O_TRUNC` while they are being read or written to, as this can forcefully truncate objects in use.

* Do not directly overwrite existing objects with an offset of 0. Adjust the write logic to prevent interception scenarios.


<span id="65303c72"></span>
### Issue: Failed to delete an object in the mount directory

What it means:


* The `tos_allow_delete` parameter was not included when mounting, which led to limited delete permissions.

* The object that you want to delete is being read or written by other processes concurrently.


How to fix it:


* Make sure the `tos_allow_delete` parameter is set correctly in the mount command. If necessary, remount the bucket.

* Check if other processes are accessing the object. Stop any related read or write operations and try deleting again.


<span id="6e064be0"></span>
### Issue: Failed to append data to an object

What it means:


* The `tos_incremental_upload` parameter was not included when mounting, so append\-only writes are not enabled.

* The remote data changed due to the simultaneous alterations made during the appending process, which led to an append failure.


How to fix it:


* Add `tos_incremental_upload` to the mount command. Then, remount the bucket and append data to the object again.

* During append\-only writes, avoid making other concurrent modifications to the same object.


<span id="2bc7142a"></span>
## Disk usage

<span id="fa7517a0"></span>
### Issue: Why is disk space being fully occupied during read and write operations in FSX?

What it means:


* By default, FSX temporarily writes data to the `/tmp/` directory. If the size of the data exceeds the available disk space, the disk may fill up.

* Similarly, in read cache scenarios, if the configured read cache space exceeds the available disk space, the disk may also become fully occupied.


How to fix it:


* The temporary file directory used for writing data must be at least 10,240 times the size of a part. For example, if the default part size is 8 MB, the temporary file directory requires 80 GiB of space. Therefore, ensure that the disk has more than 80 GiB of space.

* For read cache scenarios, make sure the configured `max_read_cache_size` (the maximum space the read cache can occupy) is smaller than the available disk space.

* When both the read and write caches are enabled, reserve at least 120 GiB of disk space for FSX. To avoid competing with other system applications for disk space, allocate a separate partition for it. For more information, see [Mount parameters](https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description).


<span id="bd0859b1"></span>
### Issue: Why does the df command show the disk space size as 8.0 EB?

What it means:

The disk usage reported by the `df` command is static and does not reflect the amount of space in the bucket. Specifically, `Size` (total disk space) and `Avail` (available disk space) are both fixed at 8 EB, while `Used` (used disk space) is fixed at 0.

How to fix it:

Avoid using the output of the `df` command to determine the actual disk usage of the bucket.

<span id="798042df"></span>
## Others

If you encounter other issues while using FSX, try [troubleshooting with FSX logs](https://docs.byteplus.com/docs/tos/FSX_logs). If that does not work, reach out to us and send us the logs.
