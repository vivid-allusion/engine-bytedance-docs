---
title: "HDFS monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs-HDFS_monitoring_metrics"
---

This document provides detailed information about HDFS metrics.

HDFS metrics include the following sections:


* [Overview](https://docs.byteplus.com/docs/E-MapReduce/105458#%E6%A6%82%E8%A7%88)

* [HDFS-NameNode](https://docs.byteplus.com/docs/E-MapReduce/105458#hdfs-namenode)

* [HDFS-DataNode](https://docs.byteplus.com/docs/E-MapReduce/105458#hdfs-datanode)


<span id="概览"></span>
## Overview


|**Title** |**metric name** |**Unit** |
|---|---|---|
|Process information |Total number of NameNode nodes |count |
||Total number of DataNode nodes |count |
||Number of active DataNode nodes |count |
||Number of inactive DataNode nodes |count |
||Number of HDFS nodes that are take down but live |count |
||Number of HDFS nodes that are take down but dead |count |
||Number of DataNode nodes in decommissioning state |count |
||Number of DataNode nodes marked as stale due to heartbeat delay |count |
|Block status |Total number of HDFS blocks |count |
||BLOCK capacity |count |
||Number of HDFS blocks waiting to be backed up |count |
||Number of HDFS blocks with fewer than the required replicas |count |
||Number of HDFS bad blocks |count |
||Number of HDFS blocks scheduled for backup |count |
||Number of HDFS blocks waiting to be deleted |count |
||Number of HDFS blocks exceeding the replica count |count |
||Number of HDFS lost blocks |count |
||Number of HDFS blocks deferred for processing at startup |count |
|Storage status |Total storage capacity |GB |
||DFS storage usage |GB |
||Remaining HDFS space |GB |
||Non\-DFS storage usage |GB |
||DFS storage utilization |% |
||Minimum DataNode storage utilization |% |
||Maximum DataNode storage utilization |% |
||Standard deviation of DataNode storage usage | |
|Cluster load |Number of HDFS cluster client connections |count |
||Number of HDFS cluster files |count |
||HDFS Snapshots |count |
||Total number of HDFS bad disks |count |


<span id="hdfs-namenode"></span>
## HDFS\-NameNode


|**Title** |**metric name** |**Unit** |
|---|---|---|
|Data throughput |NameNode data receive rate |Bytes/s |
||NameNode data send rate |Bytes/s |
|QPS |NameNode RPC call rate |times/s |
|Request processing latency |Average RPC latency |ms |
||Average RPC request processing time |ms |
|Authentication and authorization |Number of RPC authentication failures |count |
||Number of RPC authentication successes |count |
||RPC authorization failure count |count |
||RPC authorization success count |count |
|Current number of connections |Current connection count |count |
|RPC queue length |NameNode RPC call queue length |count |
||LockQueueLength file lock wait queue length |count |
|JVM heap memory status |current size of non\-heap memory used by JVM |MB |
||Current size of JVM NonHeapMemory committed |MB |
||current size of heap memory used by JVM |MB |
||Current size of JVM HeapMemory committed |MB |
||configured size of heap memory in JVM |MB |
||maximum memory size available to JVM at runtime |MB |
|Block report latency |Average latency for processing DataNode blocks per second |count |
|number of JVM threads |number of threads in NEW state |count |
||number of threads in RUNNABLE state |count |
||number of threads in BLOCKED state |count |
||number of threads in WAITING state |count |
||number of threads in TIMED WAITING state |count |
||number of threads in Terminated state |count |
||Peak thread count |count |
||Thread count |count |
||number of background threads |count |
|number of JVM logs |Number of FATAL level logs |count |
||Number of ERROR level logs |count |
||Number of WARN level logs |count |
||Number of INFO level logs |count |
|number of GC events |number of Young GC events |count |
||number of Full GC events |count |
|GC duration |NameNode JVM total GC time statistics |s |
||NameNode JVM FGC time statistics |s |
||NameNode JVM YGC time statistics |s |
|Memory region usage ratio |Survivor 0 region memory usage ratio | |
||Survivor 1 region memory usage ratio | |
||Eden region memory usage ratio | |
||Old region memory usage ratio | |
||Metaspace region memory usage ratio | |
||Compressed class space region memory usage ratio | |
||Code Cache region usage | |
||NameNode JVM memory partition usage | |
|Number of storage units marked as expired |Total number of storage directories for all expired DataNodes |count |
|Number of messages pending on standby NameNode related to BLOCK related operations |Number of DataNode requests queued in standby NameNode |count |
|Missing block statistics |Number of missing data blocks |count |
||Number of missing databases (rf = 1) |count |
|SNAPSHOT operations |Number of AllowSnapshot operations executed per second |count |
||Number of DisallowSnapshot operations executed per second |count |
||Number of CreateSnapshot operations executed per second |count |
||Number of DeleteSnapshot operations executed per second |count |
||Number of ListSnapshottableDir operations executed per second |count |
||Number of SnapshotDiffReportOps operations executed per second |count |
||Number of RenameSnapshotOps operations executed per second |count |
|File operations |Number of CreateFile operations executed per second |count |
||Number of GetListing operations executed per second |count |
||Number of TotalFileOps operations executed per second |count |
||Number of DeleteFile operations executed per second |count |
||Number of FileInfo operations executed per second |count |
||Number of GetAdditionalDatanode operations executed per second |count |
||Number of CreateSymlink operations executed per second |count |
||Number of GetLinkTarget operations executed per second |count |
||Number of FilesInGetListing operations executed per second |count |
|File statistics |Number of files and folders deleted or renamed |count |
||Number of files and folders created |count |
||Number of appended files |count |
|Transaction operations |Number of journal transaction operations processed per second |times |
||Number of journal transaction operations processed in batch per second |times |
||Average latency for processing journal transaction operations |ms |
||Total number of transactions since last checkpoint |count |
|Image operations |Number of GetEditNumOps operations executed per second |count |
||Number of GetImageNumOps operations executed per second |count |
||Number of PutImageNumOps operations executed per second |count |
||Average latency for reading Edit file operations |ms |
||Average latency for reading image files |ms |
||Average latency for writing image files |ms |
|SYNC operations |Number of Journal syncs operations processed per second |count |
||Average latency for processing Journal syncs operations |ms |
|Block operations |Number of BlockReceivedAndDeletedOps operations processed per second |times |
||Number of HDFS Block Ops in Queued state |count |
||Number of DataNode Block report operations processed per second |times |
|Cache report |Number of CacheReport operations processed per second |times |
||Average latency for cache report actions |ms |
|Startup time |Process startup time |ms |
|Checkpoint |Time since last Checkpoint |time |
|RPC average time (1) |Average latency for Complete requests |ms |
||Average latency for Create requests |ms |
||Average latency for Rename requests |ms |
||Average latency for AddBlock requests |ms |
||Average latency for GetListing requests |ms |
||Average latency for GetFileInfo requests |ms |
||Average latency for SendHeartbeat requests |ms |
|RPC average time (2) |Average latency for RegisterDatanode requests |ms |
||Average latency for BlockReport requests |ms |
||Average latency for Delete requests |ms |
||Average latency for RenewLease requests |ms |
||Average latency for BlockReceivedAndDeleted requests |ms |
||Average latency for Fsync requests |ms |
||Average latency for VersionRequest requests |ms |
|RPC average time (3) |Average latency for ListEncryptionZones requests |ms |
||Average latency for SetPermission requests |ms |
||Average latency for SetTimes requests |ms |
||Average latency for SetSafeMode requests |ms |
||Average latency for Mkdirs requests |ms |
||Average latency for GetServerDefaults requests |ms |
||Average latency for GetBlockLocations requests |ms |
|Safe mode |Whether the NameNode process is not in safe mode<br><br>1 indicates not in safe mode, 0 indicates in safe mode. | |


<span id="hdfs-datanode"></span>
## HDFS\-DataNode


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|XCEIVER count |DataNode XCEIVER count |count |
|Data read/write rate |DataNode local write rate |Bytes/s |
||DataNode local read rate |Bytes/s |
||DataNode remote write rate |Bytes/s |
||DataNode remote read rate |Bytes/s |
|Client connection count |Remote client write operation QPS |times/s |
||Local client write operation OPS |times/s |
||Remote client read operation QPS |times/s |
||Local client read operation QPS |times/s |
|Block operations and verification |Number of BLOCK verification failures |count |
||Block OPS read from DataNode |times/s |
||Block OPS written to DataNode |times/s |
||OPS for DataNode checksum operations |times/s |
||OPS for Block replication operations |times/s |
||OPS for Replace Block operations |times/s |
||OPS for BLOCK report actions |times/s |
||OPS for BLOCK incremental reports |times/s |
||OPS for cache reports |times/s |
||Number of ACK ROUND TRIP processed per second |times/s |
|Failures and errors |Number of disk failures |count |
||number of network errors |count |
|heartbeat |average time for the heartbeat interface |ms |
||heartbeat interface QPS |times/s |
|packet transmission |average time for sending data packets |ns |
|data block operation duration |average time for block read operation |ms |
||average time for block write operation |ms |
||average time for block verification operation |ms |
||average time for block copy operation |ms |
||average time for Replace Block operation |ms |
||average block report time |ms |
||average incremental block report time |ms |
||average cache report time |ms |
||average time for processing ACK ROUND TRIP |ms |
|FSYNC and Flush operations |number of FSYNC operations processed per second |times/s |
||number of Flush operations processed per second |times/s |
||average time for Flush operation |ms |
||average time for Fsync operation |ms |
|RAMDISK block processing and read/write |total number of blocks written to memory |blocks |
||total number of blocks written to memory but not successful (failover to disk) |blocks |
||total number of blocks deleted by the application before being Save to disk |blocks |
||total number of times blocks in memory are read |blocks |
||total number of blocks cleared from memory |blocks |
||total number of unread blocks cleared from memory |blocks |
||total number of blocks written to disk by lazy writer |blocks |
||total number of bytes written to disk by lazy writer |Bytes |
||total number of bytes written to memory |Bytes |
|JVM memory status |current size of non\-heap memory used by JVM |MB |
||configured size of non\-heap committed memory in JVM |MB |
||current size of heap memory used by JVM |MB |
||JVM heap memory committed size |MB |
||configured size of heap memory in JVM |MB |
||maximum memory size available to JVM at runtime |MB |
|number of JVM threads |number of threads in NEW state |count |
||number of threads in RUNNABLE state |count |
||number of threads in BLOCKED state |count |
||number of threads in WAITING state |count |
||number of threads in TIMED WAITING state |count |
||number of threads in Terminated state |count |
||peak number of threads |count |
||number of background threads |count |
|number of JVM logs |number of Fatal logs |count |
||number of Error logs |count |
||number of Warn logs |count |
||number of Info logs |count |
|number of GC events |number of Young GC events |count |
||number of Full GC events |count |
|GC duration |Full GC duration |s |
||total GC duration |s |
||Young GC duration |s |
|memory region usage ratio |Survivor region memory usage ratio |% |
||Eden region memory usage ratio |% |
||Old region memory usage ratio |% |
||Metaspace region memory usage ratio |% |
||Compressed class space region memory usage ratio |% |
|RPC |RPC call rate |times/s |
||Average duration of RPC in queued state | |
||Average RPC processing time | |
||RPC processing queue length | |
|Data throughput |Receiving data rate |Bytes/s |
||Sending data rate |Bytes/s |
|Authentication and authorization |RPC authentication failure count |count |
||RPC authentication success count |count |
||RPC authorization failure count |count |
||RPC authorization success count |count |
|Number of connections |Current number of connections |count |
|CPU |HDFS DataNode CPU system time |ms |
||HDFS DataNode CPU user time |ms |
|Startup time |Process startup time |s |
