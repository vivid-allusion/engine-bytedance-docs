---
title: "DataFlow FAQ"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DataFlow_FAQ"
---

This topic addresses common questions about EFS DataFlow.

<span id="HPfrmOwX"></span>
## How can I view the bandwidth statistics for DataFlow import or export policies?

You can find this information by selecting the **Monitoring alarm** tab on the file system details page. Steps:


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Monitoring alarm**.

6. On the **Monitoring alarm** page, select the **Bandwidth information** or **QPS information** tab to view relevant data. For more information, see [EFS monitoring metrics](https://docs.byteplus.com/en/docs/nas/efs_Creating_alarm_strategies#3sJZKQos).


<span id="vvk3s1gR"></span>
## Why does an `ESTALE` error occur temporarily when I try to access a file that clearly exists, and why does this error disappear when I try again?


* Cause

   Running an import or eviction task modifies the metadata of files in EFS. If your workload accesses a file while a task is processing it, a metadata operation conflict may occur. This can result in failed access and an `ESTALE` (stale file handle) error.

* Solution

   * **Import scenarios**: Run the import task before the workload begins accessing data. Ensure that all data is fully loaded into EFS before serving it.

   * **Eviction scenarios**: Adjust the execution schedule to avoid performing eviction operations during peak workload hours.

   * **Workaround**: If you cannot separate task execution from workload activity, close and reopen the file that returned the `ESTALE` error. Then, try accessing it again.

* Notes

   If the issue persists, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000244) to contact our technical team.


<span id="EmDOIjVf"></span>
## Why does a file exist yet continuously return an `ESTALE` error when accessed? It remains inaccessible no matter how many times I try.


* Cause

   If the data has not been imported into the EFS file system and only the metadata exists, and if the corresponding object in the TOS bucket has been deleted, Lazyload operations will persistently return an `ESTALE` error.

* Solution

   Check the lifecycle rule configuration of the TOS bucket to see if the object was deleted prematurely due to an overly short retention period. If you need to keep the data, adjust the rule and rerun the import task.


<span id="Ztfyjga4"></span>
## How can I check whether a file has been successfully imported into EFS or exported to TOS?

DataFlow **log analysis** lets you view and query real\-time records of all import and export tasks. You can turn on this feature to check task status in the following ways:


* You can enable the log analysis feature when creating a DataFlow policy. For instructions, see [Creating DataFlow policies](https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_policies#hgQLhtsU).

* You can also enable the log analysis feature for existing DataFlow policies. For instructions, see [Enable log analysis (Optional)](https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs#5nLJHj9S).


The **Log analysis** tab of the DataFlow policy details page will show you task logs once this feature is enabled. For more information, see [Viewing DataFlow logs](https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs).

<span id="BeBJisY6"></span>
## What causes the import of files to EFS or the export of files to TOS to fail?


* Note: Expected latency

   * The automatic import and export process takes a few **minutes**, and this time may increase as the number of files and the cluster workload grow.

   * The time taken to import or export large files increases linearly with file size, with extra\-large files potentially taking **hours** to complete.

* Troubleshooting common failures

   If tasks involving small files take more than 30 minutes to execute and the DataFlow log analysis feature is enabled, you can search the log field `file_name` for logs indicating failures. Based on these logs, you can determine if any of the following causes apply:

   
   |**Cause** |**Description** |
   |---|---|
   |Conflict between a file and directory with the same prefix |A file and a directory with the same name exist under the same prefix in the TOS bucket. |
   |Overly long file path |The total length of the TOS file path must not exceed 1,024 bytes, and each directory or file name must not exceed 256 bytes. |
   |Illegal character encoding |The file path contains characters that are not encoded in `UTF-8`. |
   |File skipped due to the Skip Existing Files policy (Not a fault) |If you have configured your import or export task to **Skip Existing Files**, the system will intentionally skip a file if one with the same name already exists at the destination. |
   |Unsupported object types |DataFlow does not support exporting directories to TOS or importing objects that end with a slash (/) into EFS. |
   

* Notes

   For more restrictions about using DataFlow, see [Constraints and limitations](https://docs.byteplus.com/en/docs/nas/EFS_DataFlow_overview#tcAgQ8Tq).


<span id="Di6rVxTR"></span>
## What should I do if the performance pressure from DataFlow import or export tasks impacts TOS?

Currently, the available bandwidth for DataFlow is limited by the file system's bandwidth. By default, DataFlow can use up to 30% of the maximum bandwidth of the file system. The capability to flexibly control and adjust DataFlow bandwidth is under development and will be available in a future release.

<span id="ewgcaQZb"></span>
## Why does the displayed used capacity exceed the actual used capacity after I enabled automatic eviction?

When files are evicted, DataFlow records additional metadata, including the time the file was accessed. This metadata uses a minimal amount of storage space proportional to the number of files managed by DataFlow policies.

<span id="l4V5qeSM"></span>
## How can I export the same data from an EFS file system to multiple TOS buckets? Also, how can I import the same data from a TOS bucket into multiple EFS file systems?

You can create **custom DataFlow tasks manually** to transfer the same data to each TOS bucket or EFS file system individually.

<span id="jCuKiDoI"></span>
## Why does accessing large files sometimes take so long?


* Cause

   If the file's data only exists in TOS, then it must be read from TOS via Lazyload. This results in a relatively long I/O path. High latency may occur if the workload is reading the file for the first time.

* Solution

   For latency\-sensitive workloads, import large files to the EFS file system in advance.


<span id="BQxebHmd"></span>
## Why aren't operations on TOS synchronized with EFS?

Currently, DataFlow only synchronizes the following TOS events:


* tos:ObjectCreated:Put

* tos:ObjectCreated:Post

* tos:ObjectCreated:Origin

* tos:ObjectCreated:Fetch

* tos:ObjectCreated:Copy

* tos:ObjectCreated:CompleteUpload

* tos:ObjectReplication:ObjectCreated

* tos:ObjectReplication:ObjectModified

* tos:ObjectRemoved:Delete

* tos:ObjectRemoved:DeleteMarkerCreated

* tos:LifecycleExpiration:Delete

* tos:LifecycleExpiration:DeleteMarkerCreated


For more restrictions about using DataFlow, see [Constraints and limitations](https://docs.byteplus.com/en/docs/nas/EFS_DataFlow_overview#tcAgQ8Tq).

<span id="7Hs5tPsp"></span>
## Why do unexpected changes occur when data is transferred between a TOS bucket and an EFS file system?


* Cause

   DataFlow is currently available for FileNAS, EFS, and vePFS. Check if the same TOS bucket is associated with multiple file storage services, as this can cause unexpected changes to your data.

* Solution

   We recommend configuring different destination paths for DataFlow policies used by different services to prevent data from being overwritten.


<span id="h5fMzod5"></span>
## Why does a hard\-linked file become inaccessible after a custom import task is executed?

This issue occurs due to the interaction between how hard links work and how DataFlow imports are implemented.

Hard links share the same **inode** and point to the same data blocks. Multiple hard\-linked files are essentially different access points to the same data. When you import one of these files from TOS using the DataFlow feature, EFS creates a new, independent file and writes the data into it. At this point, the new file has its own inode, which **breaks the original hard\-link relationship**. Consequently, you cannot access the imported data using the hard\-linked files that were not imported.

<span id="oSFt1GEx"></span>
## Why do errors occur when exporting data to or performing Lazyload from a TOS bucket without versioning enabled?


* Cause

   When versioning is not enabled for a TOS bucket and a file with the same name is overwritten, the original version is deleted immediately. Consequently, DataFlow operations cannot locate the necessary object version, which results in failure. Common scenarios include:

   * **Scenario 1: On‑demand load failures**

      Once an import task from TOS to EFS is complete, uploading a new object with the same name to overwrite the original in TOS requires rerunning the import task to synchronize the new version with EFS. Triggering a Lazyload for the file from the EFS side before the reimport process is complete may cause the operation to fail. This occurs because the original object version has been overwritten and deleted while the new version has not yet been synchronized with EFS. This makes it impossible for EFS to locate the corresponding version.

   * **Scenario 2: Export failures**

      Export operations may fail after a file has been imported and the object with the same name in TOS is later overwritten, because the export operation still needs the original object version, which has already been removed.

* Solution

   If your workload requires Lazyload and involves frequent updates to objects with identical names, we recommend enabling versioning on the TOS bucket. Once enabled, TOS will retain historical versions of objects and perform DataFlow operations (import, export, and Lazyload) on the correct version. This prevents failures caused by overwriting objects.
