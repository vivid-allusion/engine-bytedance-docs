---
title: "Celeborn monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_celeborn_monitoring_metrics"
---

This document provides detailed information about Celeborn metrics.

Celeborn metrics include the following sections:


* [Celeborn overview](https://docs.byteplus.com/docs/E-MapReduce/105447#celeborn-%E6%A6%82%E8%A7%88)

* [Celeborn Master](https://docs.byteplus.com/docs/E-MapReduce/105447#celeborn-master)

* [Celeborn Worker](https://docs.byteplus.com/docs/E-MapReduce/105447#celeborn-worker)


<span id="celeborn-概览"></span>
## Celeborn overview


|**Dimension** |metric name |Unit |
|---|---|---|
|Service overview |Number of active Celeborn Workers |count |
||Number of Celeborn Workers with lost heartbeat |count |
||Number of abnormal Celeborn Workers |count |
||Number of ongoing Celeborn Shuffles |count |
||Number of running Celeborn Apps |count |
||Average size of Celeborn Partitions |MB |
||Total write size of Celeborn Partitions |MB |
||Number of Celeborn Partition files |count |


<span id="celeborn-master"></span>
## Celeborn Master


|**Dimension** |metric name |Unit |
|---|---|---|
|Active Master |Celeborn Active Master node status |times |
|OfferSlots |Number of Celeborn OfferSlots |times |
||Maximum duration of Celeborn OfferSlots |ms |
||Average duration of Celeborn OfferSlots |ms |
||Minimum duration of Celeborn OfferSlots |ms |
||P50 duration of Celeborn OfferSlots |ms |
||P75 duration of Celeborn OfferSlots |ms |
||P90 duration of Celeborn OfferSlots |ms |
||P98 duration of Celeborn OfferSlots |ms |
||P99 duration of Celeborn OfferSlots |ms |
||P999 duration of Celeborn OfferSlots |ms |
|JVM memory metrics |Celeborn Master heap committed size |MB |
||Celeborn Master heap usage rate |% |
||Celeborn Master heap used size |MB |
||Celeborn Master maximum heap size |MB |
||Celeborn Master non\-heap memory used size |MB |
||Celeborn Worker non\-heap memory committed size |MB |
||Celeborn Master Young GC count |times |
||Celeborn Master Young GC duration |ms |
||Celeborn Master Full GC count |times |
||Celeborn Master Full GC duration |ms |
|Direct memory metrics |Number of Celeborn Master Direct memory blocks |count |
||Celeborn Master Direct memory capacity |MB |
||Celeborn Master Direct memory usage |MB |
|Mapped memory metrics |Number of Celeborn Master Mapped memory blocks |count |
||Celeborn Master Mapped memory capacity |MB |
||Celeborn Master Mapped memory usage |MB |
|System metrics |Celeborn Master JVM CPU Time |ms |
||Celeborn Master machine CPU usage in the last minute |% |
||Number of available cores on Celeborn Master machine |count |


<span id="celeborn-worker"></span>
## Celeborn Worker


|**Dimension** |metric name |Unit |
|---|---|---|
|Active Shuffle metrics |Current number of Celeborn Worker connections |count |
||Number of registered Shuffles on Celeborn Worker |count |
||Data size of currently active Shuffles on Celeborn Worker |MB |
||Number of currently active Shuffle files on Celeborn Worker |count |
||Number of currently active MapPartition files on Celeborn Worker |count |
|Statistics of data write failures |Number of write failures on Celeborn Worker |count |
|Statistics of primary file write failure requests |Number of Celeborn Worker Flink region write failures (start) |count |
||Number of Celeborn Worker Flink region write failures (finish) |count |
||Number of handshake failures during PushData |count |
|PrimaryPushData |Number of Celeborn PrimaryPushData |count |
||Maximum duration of Celeborn PrimaryPushData |ms |
||Average duration of Celeborn PrimaryPushData |ms |
||Minimum duration of Celeborn PrimaryPushData |ms |
||P50 duration of Celeborn PrimaryPushData |ms |
||P75 duration of Celeborn PrimaryPushData |ms |
||P95 duration of Celeborn PrimaryPushData |ms |
||P98 duration of Celeborn PrimaryPushData |ms |
||P99 duration of Celeborn PrimaryPushData |ms |
||P999 duration of Celeborn PrimaryPushData |ms |
|PrimaryPushDataHandshake |Number of Celeborn PrimaryPushDataHandshake |times |
||Maximum duration of Celeborn PrimaryPushDataHandshake |ms |
||Average duration of Celeborn PrimaryPushDataHandshake |ms |
||Minimum duration of Celeborn PrimaryPushDataHandshake |ms |
||P50 duration of Celeborn PrimaryPushDataHandshake |ms |
||P75 duration of Celeborn PrimaryPushDataHandshake |ms |
||P95 duration of Celeborn PrimaryPushDataHandshake |ms |
||P98 duration of Celeborn PrimaryPushDataHandshake |ms |
||P99 duration of Celeborn PrimaryPushDataHandshake |ms |
||P999 duration of Celeborn PrimaryPushDataHandshake |ms |
|PrimaryRegionFinish |Number of Celeborn PrimaryRegionFinish |times |
||Maximum duration of Celeborn PrimaryRegionFinish |ms |
||Average duration of Celeborn PrimaryRegionFinish |ms |
||Minimum duration of Celeborn PrimaryRegionFinish |ms |
||P50 duration of Celeborn PrimaryRegionFinish |ms |
||P75 duration of Celeborn PrimaryRegionFinish |ms |
||P95 duration of Celeborn PrimaryRegionFinish |ms |
||P98 duration of Celeborn PrimaryRegionFinish |ms |
||P99 duration of Celeborn PrimaryRegionFinish |ms |
||P999 duration of Celeborn PrimaryRegionFinish |ms |
|PrimaryRegionStart |Number of Celeborn PrimaryRegionStart |times |
||Maximum duration of Celeborn PrimaryRegionStart |ms |
||Average duration of Celeborn PrimaryRegionStart |ms |
||Minimum duration of Celeborn PrimaryRegionStart |ms |
||P50 duration of Celeborn PrimaryRegionStart |ms |
||P75 duration of Celeborn PrimaryRegionStart |ms |
||P95 duration of Celeborn PrimaryRegionStart |ms |
||P98 duration of Celeborn PrimaryRegionStart |ms |
||P99 duration of Celeborn PrimaryRegionStart |ms |
||P999 duration of Celeborn PrimaryRegionStart |ms |
|Replica data read count |Number of Celeborn replica data reads |times |
|Statistics of replica failure requests |Number of Celeborn ReplicateDataWriteFail |count |
||Celeborn ReplicateDataConnectionException times |count |
||Celeborn ReplicateDataCreateConnectionFail times |count |
||Celeborn ReplicateDataTimeout times |count |
|ReplicaPushDataHandshake |Celeborn ReplicaPushDataHandshake times |times |
||Celeborn ReplicaPushDataHandshake maximum duration |ms |
||Celeborn ReplicaPushDataHandshake average duration |ms |
||Celeborn ReplicaPushDataHandshake minimum duration |ms |
||Celeborn ReplicaPushDataHandshake duration P50 |ms |
||Celeborn ReplicaPushDataHandshake duration P75 |ms |
||Celeborn ReplicaPushDataHandshake duration P95 |ms |
||Celeborn ReplicaPushDataHandshake duration P98 |ms |
||Celeborn ReplicaPushDataHandshake duration P99 |ms |
||Celeborn ReplicaPushDataHandshake duration P999 |ms |
|ReplicaRegionFinish |Celeborn ReplicaRegionFinish times |times |
||Celeborn ReplicaRegionFinish maximum duration |ms |
||Celeborn ReplicaRegionFinish average duration |ms |
||Celeborn ReplicaRegionFinish minimum duration |ms |
||Celeborn ReplicaRegionFinish duration P50 |ms |
||Celeborn ReplicaRegionFinish duration P75 |ms |
||Celeborn ReplicaRegionFinish duration P95 |ms |
||Celeborn ReplicaRegionFinish duration P98 |ms |
||Celeborn ReplicaRegionFinish duration P99 |ms |
||Celeborn ReplicaRegionFinish duration P999 |ms |
|ReplicaRegionStart |Celeborn ReplicaRegionStart times |times |
||Celeborn ReplicaRegionStart maximum duration |ms |
||Celeborn ReplicaRegionStart average duration |ms |
||Celeborn ReplicaRegionStart minimum duration |ms |
||Celeborn ReplicaRegionStart duration P50 |ms |
||Celeborn ReplicaRegionStart duration P75 |ms |
||Celeborn ReplicaRegionStart duration P95 |ms |
||Celeborn ReplicaRegionStart duration P98 |ms |
||Celeborn ReplicaRegionStart duration P99 |ms |
||Celeborn ReplicaRegionStart duration P999 |ms |
|ReplicaPushData |Celeborn ReplicaPushData times |times |
||Celeborn ReplicaPushData maximum duration |ms |
||Celeborn ReplicaPushData average duration |ms |
||Celeborn ReplicaPushData minimum duration |ms |
||Celeborn ReplicaPushData duration P50 |ms |
||Celeborn ReplicaPushData duration P75 |ms |
||Celeborn ReplicaPushData duration P95 |ms |
||Celeborn ReplicaPushData duration P98 |ms |
||Celeborn ReplicaPushData duration P99 |ms |
||Celeborn ReplicaPushData duration P999 |ms |
|CommitFiles |Celeborn CommitFiles times |times |
||Celeborn CommitFiles maximum duration |ms |
||Celeborn CommitFiles average duration |ms |
||Celeborn CommitFiles minimum duration |ms |
||Celeborn CommitFiles duration P50 |ms |
||Celeborn CommitFiles duration P75 |ms |
||Celeborn CommitFiles duration P95 |ms |
||Celeborn CommitFiles duration P98 |ms |
||Celeborn CommitFiles duration P99 |ms |
||Celeborn CommitFiles duration P999 |ms |
|CreditStream |Celeborn CreditStream count |count |
|FetchChunk |Celeborn FetchChunk times |times |
||Celeborn FetchChunk maximum duration |ms |
||Celeborn FetchChunk average duration |ms |
||Celeborn FetchChunk minimum duration |ms |
||Celeborn FetchChunk duration P50 |ms |
||Celeborn FetchChunk duration P75 |ms |
||Celeborn FetchChunk duration P95 |ms |
||Celeborn FetchChunk duration P98 |ms |
||Celeborn FetchChunk duration P99 |ms |
||Celeborn FetchChunk duration P999 |ms |
|OpenStream |Celeborn OpenStream times |times |
||Celeborn OpenStream maximum duration |ms |
||Celeborn OpenStream average duration |ms |
||Celeborn OpenStream minimum duration |ms |
||Celeborn OpenStream duration P50 |ms |
||Celeborn OpenStream duration P75 |ms |
||Celeborn OpenStream duration P95 |ms |
||Celeborn OpenStream duration P98 |ms |
||Celeborn OpenStream duration P99 |ms |
||Celeborn OpenStream duration P999 |ms |
|Pause information |Celeborn PausePushData times |times |
||Celeborn PausePushDataAndReplicate times |times |
||Celeborn PausePushData duration |ms |
|Slots information |Celeborn number of Slots allocated in the past hour |count |
||Celeborn ReserveSlots times |times |
||Celeborn ReserveSlots maximum duration |ms |
||Celeborn ReserveSlots average duration |ms |
||Celeborn ReserveSlots minimum duration |ms |
||Celeborn ReserveSlots duration P50 |ms |
||Celeborn ReserveSlots duration P75 |ms |
||Celeborn ReserveSlots duration P95 |ms |
||Celeborn ReserveSlots duration P98 |ms |
||Celeborn ReserveSlots duration P99 |ms |
||Celeborn ReserveSlots duration P999 |ms |
|Shuffle sort information |Celeborn memory resources reserved in memory for Shuffle files that require sorting |MB |
||Celeborn Shuffle files being sorted or prepared for sorting |count |
||Celeborn number of Shuffle files already sorted |count |
||Celeborn size of Shuffle files already sorted |MB |
||Celeborn Shuffle file sorting times |times |
||Celeborn maximum duration for Shuffle sorting |ms |
||Celeborn average duration for Shuffle sorting |ms |
||Celeborn minimum duration for Shuffle sorting |ms |
||Celeborn Shuffle file sorting duration P50 |ms |
||Celeborn Shuffle file sorting duration P75 |ms |
||Celeborn Shuffle file sorting duration P95 |ms |
||Celeborn Shuffle file sorting duration P98 |ms |
||Celeborn Shuffle file sorting duration P99 |ms |
||Celeborn Shuffle file sorting duration P999 |ms |
|Flush metrics |Celeborn size of Shuffle data pending disk write |MB |
||Celeborn FlushData times |times |
||Celeborn FlushData maximum duration |ms |
||Celeborn FlushData average duration |ms |
||Celeborn FlushData minimum duration |ms |
||Celeborn FlushData duration P50 |ms |
||Celeborn FlushData duration P75 |ms |
||Celeborn FlushData duration P95 |ms |
||Celeborn FlushData duration P98 |ms |
||Celeborn FlushData duration P99 |ms |
||Celeborn FlushData duration P999 |ms |
||Celeborn TakeBuffer times |times |
||Celeborn TakeBuffer maximum duration |ms |
||Celeborn TakeBuffer average duration |ms |
||Celeborn TakeBuffer minimum duration |ms |
||Celeborn TakeBuffer duration P50 |ms |
||Celeborn TakeBuffer duration P75 |ms |
||Celeborn TakeBuffer duration P95 |ms |
||Celeborn TakeBuffer duration P98 |ms |
||Celeborn TakeBuffer duration P99 |ms |
||Celeborn TakeBuffer duration P999 |ms |
|Disk information |Celeborn total disk capacity |MB |
||Celeborn free disk capacity |MB |
||Available disk capacity configured for Celeborn |MB |
||Remaining capacity in the available disk capacity configured for Celeborn |MB |
|Netty memory usage |Direct memory size used by Celeborn Netty |MB |
||Pooled ByteBuf size allocated by Celeborn Netty for reading |MB |
||Buffer memory request count for Celeborn Netty |count |
||Pooled ByteBuf count allocated by Celeborn Netty for reading |count |
|JVM memory metrics |Committed heap size for Celeborn Worker |MB |
||Heap usage percentage for Celeborn Worker |% |
||Heap usage size for Celeborn Worker |MB |
||Maximum heap size for Celeborn Worker |MB |
||Non\-heap memory usage size for Celeborn Worker |MB |
||Committed non\-heap memory size for Celeborn Worker |MB |
|JVM GC metrics |Young GC times for Celeborn Worker |times |
||Young GC duration for Celeborn Worker |ms |
||Young GC times for Celeborn Worker |times |
||Young GC duration for Celeborn Worker |ms |
|Direct memory metrics |Direct memory block count for Celeborn Worker |count |
||Direct memory capacity for Celeborn Worker |MB |
||Direct memory usage for Celeborn Worker |MB |
|Mapped memory metrics |Mapped memory block count for Celeborn Worker |count |
||Mapped memory capacity for Celeborn Worker |MB |
||Mapped memory usage for Celeborn Worker |MB |
|System metrics |Celeborn Worker JVM CPU Time |ms |
||CPU usage percentage of the machine hosting Celeborn Worker in the last minute |% |
||Available core count on the machine hosting Celeborn Worker |count |
