---
title: "Proton SDK optimization guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_SDK_optimization_guide"
---

After creating EMR on Volcano Engine or applying Proton to a self\-built Hadoop cluster, targeted performance optimization can be performed based on different use cases.

<span id="写大文件场景"></span>
## 1 Large file write use case

When Proton writes large files, it uses the object storage MPU mechanism to perform asynchronous multipart uploads. Before each part is filled on the client side, data is preferentially written to the local disk by default. Once a part is filled, it is uploaded asynchronously to object storage, and the part data on the disk is cleared. Therefore, file write speed may be limited by the local disk write bandwidth and the upload network bandwidth. By default, the former is much higher than the latter. As a result, the write process can fully utilize multiple local disks to improve data write performance. Multi\-disk configuration can be achieved by modifying `core-site.xml` and setting `fs.tos.multipart.staging-dir`, for example:

```xml
<property>
    <name>fs.tos.multipart.staging-dir</name>
    <value>/data01/stagingdir,/data02/stagingdir,/data03/stagingdir</value>
</property>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In EMR scenarios, the configuration has already been set by default based on the disk mounting status of EMR nodes, so no additional configuration is required. Important: When manually configuring this parameter, tasks that write data must have read and write permissions for these configuration directories.</div>


Additionally, when uploading large files using MPU, since MPU has a limit of 10,000 parts, it is necessary to set an appropriate part size. For example, when writing a 100 GB object, the minimum part size is 10.24 MB. In this case, it is recommended to set the corresponding parameter `fs.tos.multipart.size` to `2^n`, that is, 16 MB.

```xml
<property>
    <name>fs.tos.multipart.size</name>
    <value>16777216</value>
    <description>默认值为8MB</description>
</property>
```


The number of threads for concurrent part uploads can also be increased to accelerate file write operations.

```xml
<property>
    <name>fs.tos.multipart.thread-pool-size</name>
    <value>64</value>
    <description>默认值为所在ECS节点核数的2倍，不建议超过超过ECS节点核数的4倍</description>
</property>
```


<span id="高并发写小文件场景"></span>
## 2 High\-concurrency small file write use case

Similar to large file writes, the client writes a batch of data locally before uploading it to object storage. In high\-concurrency small file write use cases, the client can write data directly to memory and then upload it to object storage, without the need to write to local disk. This can improve the upload speed of small files. The value of the `fs.tos.multipart.staging-buffer-size` parameter can be set as the threshold for determining which storage medium to use. When the amount of data written is less than this value, it will be written to memory; otherwise, it will be written to local disk. In production practice, when increasing this value, it is recommended to adjust the JVM heap parameters at the same time to avoid performance issues caused by frequent GC due to insufficient memory and OOM problems.

```xml
<property>
    <name>fs.tos.multipart.staging-buffer-size</name>
    <value>4096</value>
    <description>默认值为4k，单位为byte</description>
<property>
```


Meanwhile, when uploading data to object storage, you can choose between two upload modes: MPU multipart upload or direct PUT. For small file scenarios, using direct PUT improves write performance. You can configure the threshold by setting the `fs.tos.multipart.threshold` parameter. If the size of the object being written exceeds this value, MPU multipart asynchronous upload is used; if it is less than this value, direct PUT is used.

```xml
<property>
    <name>fs.tos.multipart.threshold</name>
    <value>10485760</value>
    <description>默认值为10M，不建议将该指设置的特别大，同时如果启用Job Committer场景下，会直接使用MPU</description>
</property>
```


<span id="rename大目录场景"></span>
## 3 Rename large directory scenarios

When you need to perform Rename/MV operations on a large directory, the client first lists all subfiles/subdirectories in batches under the directory, then performs Rename operations on them in parallel. You can increase the concurrency by adjusting `fs.tos.task.thread-pool-size` to improve the speed of renaming subdirectories/subfiles.

```xml
<property>
    <name>fs.tos.task.thread-pool-size</name>
    <value>64</value>
    <description>默认值为所在ECS节点核数的2倍</description>
</property>
```


By default, Proton performs Rename operations on a file using Copy + Delete. Volcano Engine TOS natively supports Rename semantics, so directly using TOS Rename semantics can significantly improve Rename performance. To use Rename semantics, you need to perform the following two operations:


1. Go to the TOS console \-\> select the object bucket \-\> Overview \-\> RenameObject \-\> Enable

2. Modify the `fs.tos.rename.enabled` parameter in `core-site.xml`.


```Bash
<property>
    <name>fs.tos.rename.enabled</name>
    <value>true</value>
    <description>默认false，开启后直接使用Rename语义代替Copy+Delete操作</description>
</property>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Since object storage itself does not support the concept of files or directories, the aforementioned Rename semantics mainly refer to renaming a single object. In business scenarios where you need to rename a large directory, you still need to first list all objects to be renamed and then perform Rename operations concurrently. To perform Rename operations directly on directories, you need to create a TOS tiered bucket (Preview).</div>


2. <div data-tips="true" data-tips-type="tip">After enabling the Rename feature in TOS, you can still perform Rename operations on objects created after a specific point in time (after enabling). Objects created before that point cannot be renamed. The specific points in time are as follows:</div>


   <div data-tips="true" data-tips-type="tip">North China 2: 2024\-07\-11 11:00   </div>
   

   <div data-tips="true" data-tips-type="tip">East China 2: 2024\-07\-04 15:00   </div>
   

   <div data-tips="true" data-tips-type="tip">South China 1: 2024\-07\-04 15:00   </div>
   

   <div data-tips="true" data-tips-type="tip">Johor: 2024\-07\-11 11:00   </div>
   


<span id="79137211"></span>
## 4 Retrieve file metadata scenarios

In big data scenarios, calling `Filesystem.getFileStatus(path)` to obtain the status information of a directory or file is a very common use cases. Since object storage itself does not have the concept of files or directories, when we use object storage as a file system, we often determine whether an object is a file or a directory based on whether the object name ends with `/`. Objects ending with `/` are often empty objects. For example, the object `a/b/c` is a file, and `a/b/c/` is a directory.

When implementing `Filesystem.getFileStatus(path)` based on object storage, it may require two headObject operations and one listObject operation to obtain the metadata of the path in object storage. This process results in the problem of increased RPC calls, especially when the object corresponding to the path does not exist. Since `Filesystem.getFileStatus(path)` is a high\-frequency operation, the RPC amplification issue becomes more severe as the number of calls increases. In extreme cases, it may reach the QPS flow control quota limit of object storage, resulting in degraded performance.

Volcano Engine TOS provides a corresponding `getFileStatus` interface for this scenario, which can merge three RPC requests into one RPC request, thereby resolving the RPC amplification issue. When accessing object storage via Proton, you need to add or modify the `core-site.xml` parameter `fs.tos.get-file-status.enabled` to use the `getFileStatus` feature.

```XML
<property>
    <name>fs.tos.get-file-status.enabled</name>
    <value>true</value>
</property>
```
