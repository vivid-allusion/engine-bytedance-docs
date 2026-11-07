---
title: "Data flow overview"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Data_Flow_overview"
---

Data Flow provides bidirectional synchronization between PFS file systems and Torch Object Storage (TOS) buckets. This topic provides you with the fundamental information about Data Flow.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Once configured between a PFS file system and a TOS bucket in the same region, Data Flow enables bidirectional data transfer. In a Export scenario, Data Flow exports data from the PFS file system to the TOS bucket. In a Import scenario, Data Flow imports data from the TOS bucket into the PFS file system. This mechanism maintains continuous synchronization of data between the two storage systems.

<span id="b0f001f2"></span>
## Specifications


|**Type** |**Specifications** |**Metrics** |**Remarks** |
|---|---|---|---|
|Compatibility |Supported file system specifications |All |\- |
|Configured bandwidth |Bandwidth range |[500 MB/s, Min (20 GB/s, Maximum write bandwidth of PFS file system)] |For 6 TiB file systems of the 100MB/s/TiB_Edition, Data Flow bandwidth is capped at 500 MB/s. |
||Step size |500 MB/s |\- |
|Import performance |Maximum Import bandwidth |Configured bandwidth |Exercise caution when transferring large files (e.g., 4 MiB) concurrently. Exceeding the limit will affect performance. |
||Maximum QPS per Import task |Min (Configured bandwidth per GB/s × 2,000, 20,000) |* For small files (e.g., 4 KiB), the higher the number of concurrent transfers, the higher the QPS.<br><br>* Maximum QPS for file\-list Import: 20,000<br><br>* Maximum QPS for path\-based Import: 12,000 |
||Maximum QPS for concurrent Import tasks |Min (Configured bandwidth (GB/s) × 2,000, 80,000) |For small files (e.g., 4 KiB), the higher the number of concurrent transfers, the higher the QPS. |
|Export performance |Maximum Export bandwidth |Configured bandwidth |Exercise caution when transferring large files (e.g., 4 MiB) concurrently. Exceeding the limit will affect performance. |
||Maximum QPS per Export task |Min (Configured bandwidth per GB/s × 2,000, 20,000) |* For small files (e.g., 4 KiB), the higher the number of concurrent transfers, the higher the QPS.<br><br>* Maximum QPS for file\-list Export: 20,000<br><br>* Maximum QPS for path\-based Export: 6,000 |
||Maximum QPS for concurrent Export tasks |min (configured bandwidth per GB/s × 2,000, 80,000) |For small files (e.g., 4 KiB), the higher the number of concurrent transfers, the higher the QPS. |
|Inventory performance |Maximum QPS per Inventory task |Min (Configured bandwidth per GB/s × 2,000, 10,000) |\- |
||Maximum QPS for concurrent Inventory tasks |Min (Configured bandwidth (GB/s) × 2,000, 80,000) ||
|Constraints on task configuration |Maximum concurrent manual tasks |10 |\- |
||Maximum number of Data Flow tasks per directory |1 |\- |
||Maximum number of files or objects per task |10 billion ||
||Maximum file system path depth |Unlimited ||
||Maximum file system path length |1,024 characters ||
||Maximum directory name length |255 characters ||
||Maximum filename length |213 characters ||
||Maximum number of files in the specified file list |* File list in TOS: 1 billion<br><br>* File list uploaded through the console: 100,000 ||
||Symbolic Link |Data Flow supports exporting Symbolic Link from PFS file systems to TOS buckets. |You can opt to ignore or export Symbolic Link as new files. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage


|**Limit** |**Restrictions** |
|---|---|
|Task configuration |* You can manually configure Data Flow tasks for filesets (subdirectories) or directories within the PFS file system.<br><br>* The PFS file system and the TOS bucket used to configure the manual task must be in the same region.<br><br>* You cannot nest the fileset (subdirectory), directory, or bucket prefix configured in a task with those in tasks that are in the **Creating**, **Running**, or **Cancelling** state. |
|File system |* Use special characters with caution. Directories and filenames can contain uppercase and lowercase letters, numbers, exclamation marks (!), hyphens (\-), underscores (_), periods (.), asterisks (\*), and parentheses (()).<br><br>* The following names will be considered invalid and will not be processed during import and export operations:<br><br>   * Names containing the `./` structures.<br><br>   * Names containing the `../` structures.<br><br>   * Names containing consecutive `/`.<br><br>   * Names ending with a single `/`.<br><br>   * Folder names exceeding 255 characters.<br><br>   * Filenames exceeding 213 characters.<br><br>   * The name only contains `.`, such as `a/b/c/...`.<br><br>* Overly long paths are not supported. Path length must be between 1 and 1,024 characters. |
|Data Flow |* Data Flow can only import data from files that are stored in TOS **Standard Storage** or **Infrequent Access Storage**.<br><br>* Data Flow can only export data to TOS **Standard Storage**.<br><br>* Data Flow cannot export directories to TOS buckets.<br><br>* Data Flow cannot export file attributes to TOS buckets.<br><br>* For sparse data, zero values are padded before they are moved to the TOS buckets.<br><br>* Data Flow cannot import Symbolic Link from TOS buckets to PFS file systems.<br><br>* Data Flow cannot export sockets, FIFOs, or block devices from PFS file systems to TOS buckets.<br><br>* Data Flow cannot export files larger than 48.8 TiB to TOS. Multipart upload supports files up to 48.8 TiB.<br><br>* The supported TOS event notification types are as follows. <br><br>   * tos:ObjectCreated:Put<br><br>   * tos:ObjectCreated:Post<br><br>   * tos:ObjectCreated:Origin<br><br>   * tos:ObjectCreated:Fetch<br><br>   * tos:ObjectCreated:Copy<br><br>   * tos:ObjectCreated:CompleteUpload<br><br>   * tos:ObjectReplication:ObjectCreated<br><br>   * tos:ObjectReplication:ObjectModified<br><br>   * tos:ObjectRemoved:Delete<br><br>   * tos:ObjectRemoved:DeleteMarkerCreated<br><br>   * tos:LifecycleExpiration:Delete<br><br>   * tos:LifecycleExpiration:DeleteMarkerCreated |


<span id="df114abb"></span>
## Notice


* Data Flow requires PFS access to TOS. Revoking this access will stop Data Flow.

* Setting the Data Flow bandwidth to 0 disables the bandwidth and stops all running Data Flow policies and tasks. However, the policies and tasks will not be deleted. Re\-configuring the Data Flow bandwidth and enabling the Data Flow policy will execute the Data Flow task again. This will overwrite the original data.

* When creating a task, make sure that the directory path is correct. If the directory doesn't exist, PFS will automatically create it.

* Data Flow relies on the file system's extended attributes (xattr) and the custom metadata capability of TOS. Exercise significant caution when cleaning up file inode\-related xattr and TOS Headers. Improper removal may result in undefined Data Flow behavior.


<span id=".5Lu75Yqh6K-05piO"></span>
## Data Flow task types


* Tasks can be divided into four categories based on the type of data operations: Import, Export, delete, and Inventory.

   
   |Task type |Note |
   |---|---|
   |Import |Imports data from a TOS bucket with a specified prefix into a specified fileset (subdirectory) or directory of a PFSile system. |
   |Export |Exports data from a specified fileset (subdirectory) or directory in a PFS file system to a TOS bucket with a specified prefix. |
   |Delete |Deletes files from PFSile systems and the associated TOS buckets.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Delete tasks are currently in preview. To create this type of task, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001286">submit a ticket</a> or contact your account manager.</div><br> |
   |Inventory |Inventory tasks only verify files within the designated directories of PFSile systems and TOS buckets. They do not execute any import or export operations. |
   

* Tasks can be divided into manual and system tasks based on how the tasks are initiated.

   
   |Task type |Note |
   |---|---|
   |Manual task |Tasks created via the console or OpenAPI. |
   |System task<br><br>(Coming soon) |Tasks automatically generated through Data Flow policies. When the **Data update automatic Import** or **Data update automatic Export** feature is enabled in a Data Flow policy, PFSutomatically initiates the corresponding transfer tasks upon detecting updates in either the TOS bucket or the PFS file system. |
   


<span id=".5L2_55So5rWB56iL"></span>
## Workflow


1. [Create a PFS file system](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system)

2. [Create a fileset](https://docs.byteplus.com/en/docs/pfs/Managing-fileset#.5Yib5bu6LWZpbGVzZXQ=)

3. [Configure data flow bandwidth](https://docs.byteplus.com/en/docs/pfs/Configure_data_flow_bandwidth)

4. [Creating manual tasks](https://docs.byteplus.com/en/docs/pfs/Creating_manual_tasks)

5. [Managing manual tasks](https://docs.byteplus.com/en/docs/pfs/Managing_manual_tasks)
