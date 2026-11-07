---
title: "Proton metadata synchronization"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_metadata_synchronization"
---

When Proton cache mode is enabled, Proton must synchronize the corresponding data's metadata to the Proton MetaServer before reading data; otherwise, a file not found error may occur, resulting in data read failure.

Therefore, to accelerate caching for historical data or data written directly to the underlying storage in non\-cache mode, additional operations or configurations are required to synchronize the metadata of this data to the Proton MetaServer

before it can be accessed normally.

Prior to Proton version 1.7.0, only batch metadata loading was supported. You can use the following command to synchronize the metadata of all data under the specified path to the Proton MetaServer.

```Plain
proton load -m tos://bucket/a/b/c
```


Starting from Proton version 1.7.0, an automatic metadata synchronization feature (Lazy Sync) is provided, which periodically synchronizes metadata from the underlying storage as needed.


* Periodic synchronization means that you can configure a time interval, and within this interval, metadata synchronization for the same file will occur only once.

* On\-demand synchronization means that synchronization is triggered only when metadata for a specific file needs to be accessed. If a file is not accessed, its metadata will not be synchronized.


Lazy Sync ensures that the metadata for accessed data is up\-to\-date in both the underlying storage and the MetaServer, while avoiding the one\-time synchronization of large amounts of metadata, thereby conserving MetaServer resources.

<span id="_1-lazy-sync-功能使用"></span>
## Step 1: Use the Lazy Sync feature

By default, Proton does not automatically synchronize metadata from the underlying storage to the Proton MetaServer.

To enable automatic metadata synchronization, add or modify the value of the `proton.metaserver.syncer.interval` parameter in the `proton.ini` configuration file (default value: \-1, Unit: milliseconds) based on your business needs. Details:


* When `proton.metaserver.syncer.interval < 0`, metadata for a file or directory will not be synchronized when accessing that file or directory.

* When `proton.metaserver.syncer.interval = 0`, metadata for a file or directory will be synchronized immediately when accessing that file or directory.

* `proton.metaserver.syncer.interval > 0` means that when accessing a file or directory, if the time since the last synchronization of the file or directory exceeds the configured threshold, the metadata of the file or directory will be synchronized immediately; otherwise, synchronization will not occur.


<span id="_2-最佳实践"></span>
## 2 Best practices

After enabling automatic metadata synchronization, there will be some performance overhead compared to scenarios where it is not enabled, as there may be an additional metadata alignment operation. Therefore, it is necessary to set this value appropriately based on actual business requirements to ensure data timeliness and consistency, while avoiding unnecessary performance costs.

The following describes how to set this parameter value appropriately in different scenarios.


|**Scenario** |**Scenario characteristics** |**Scenario description** |**Recommended practices** |
|---|---|---|---|
|**Scenario 1** |* Write data in non\-cache mode<br><br>* Read data in cache mode |* Upstream tasks continuously write data to the underlying storage in non\-cache mode,<br><br>* and downstream consumers, in cache mode, periodically start tasks every hour or every day to consume incremental data multiple times |Set the value of `proton.metaserver.syncer.interval`<br><br>to a fixed interval for the task. For example, if the interval is 3 minutes, set `proton.metaserver.syncer.interval=180000` |
|**Scenario 2** |* Write data in non\-cache mode<br><br>* Read data in cache mode |* Upstream tasks continuously write data to the underlying storage in non\-cache mode,<br><br>* and downstream consumers may read newly written data at any time |To ensure data consistency, set `proton.metaserver.syncer.interval=0`<br><br>, each time Proton MetaServer receives a data access request, it first synchronizes metadata from the underlying storage and then returns it to the client. |
|<span id="场景三"></span><br>#### Scenario 3 |* Write data in cache mode<br><br>* Read data in cache mode |* All read and write operations for business data are performed in Proton cache mode. |Since Proton MetaServer has already cached the metadata of all data, there is no need to enable the automatic metadata synchronization feature,<br><br>and you can set `proton.metaserver.syncer.interval=-1` |
|<span id="场景四"></span><br>#### Scenario four |* Write historical data in non\-cache mode<br><br>* Write new data in cache mode<br><br>* Read all data in cache mode |* In scenarios such as data migration or relocation, after synchronizing historical data to the underlying storage, subsequent business read and write operations on the data are all performed in cache mode. |You can first use Proton Load CLI to synchronize the metadata of historical data to Proton<br><br>MetaServer, and then set `proton.metaserver.syncer.interval=-1` to disable the automatic metadata synchronization feature. |


<span id="_3-注意事项"></span>
## 3 Important notes

The configuration of the `proton.metaserver.syncer.interval` parameter needs to be adjusted according to actual business requirements. If configured improperly, it may cause issues with data consistency and performance overhead.


* If the sync cycle is configured too long, it may lead to inconsistencies between the accessed data and the actual data, such as failing to find relevant files or reading outdated data.

* If the sync cycle is configured too short, it may result in many unnecessary sync operations, consuming account resources, especially in scenarios where object storage has quotas.
