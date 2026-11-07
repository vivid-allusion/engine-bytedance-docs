---
title: "DataFlow overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/EFS_DataFlow_overview"
---

With the DataFlow feature, you can export cold data from EFS to Torch Object Storage (TOS) or import data from TOS to EFS. This topic provides fundamental information about DataFlow.

<span id="Rw16h0hO"></span>
## Introduction

EFS DataFlow offers two configuration methods: DataFlow policies and DataFlow tasks.


|**Configuration method** |**Description** |
|---|---|
|DataFlow policy |* Default configuration (**Lazyload**)<br><br>   After a policy is created, the system loads metadata of all files within the TOS bucket or bucket prefix associated with the policy into EFS at once.<br><br>   When a user or application accesses files through EFS:<br><br>   * If data already exists in EFS, the system directly returns the data.<br><br>   * If data is absent in EFS, the system automatically loads the data from TOS to EFS. You can access the data in real time without waiting for the load to complete.<br><br>* Bidirectional DataFlow: A bidirectional data flow between EFS and TOS, based on configured rules.<br><br>* DataFlow rules: Include import, export, and eviction rules. An import rule can load either metadata or both metadata and data simultaneously.<br><br>* File conflict policy: Supports keeping the newest file. |
|DataFlow task |* Unidirectional DataFlow: A one\-time flow of data in one direction between EFS and TOS, based on selected task type and rules.<br><br>* DataFlow tasks: Include import, export, and eviction tasks. An import task loads both metadata and data simultaneously.<br><br>* File conflict policies: Include Skip Existing Files, Preserve Latest Files, and Overwrite Existing Files. |


<span id="tcAgQ8Tq"></span>
## Constraints and limitations


|**Category** |**Description** |
|---|---|
|Maximum number of DataFlow policies per file system |20. |
|Maximum number of DataFlow tasks per file system |20. Each policy executes a single task. |
|Maximum number of concurrent tasks per file system |20. |
|Maximum number of concurrent tasks per DataFlow policy |1. |
|Maximum paths per import or export task |20 |
|Object names |The following names will be considered invalid and will not be processed during import or export operations:<br><br><br>* Object names containing `./` structures.<br><br>* Object names containing `../` structures.<br><br>* Object names with multiple consecutive forward slashes (`/`).<br><br>* Object names ending with a single forward slash (`/`).<br><br>* **Folder** or **file names** exceeding 255 characters in length.<br><br>* Object names consisting solely of dots (`.`). For example, `a/b/c/...`. |
|Object size |* The maximum object size for importing is 48.8 TiB.<br><br>* Files larger than 16 TiB cannot be exported to TOS. |
|File system paths |* You can only create DataFlow policies for empty directories.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length should be between 3 and 1,024 characters.<br><br>* Nested file system paths across DataFlow policies are not supported. |
|TOS buckets/prefixes |Nested TOS prefixes across DataFlow policies are not supported. |
|TOS storage types |* Only `Normal` TOS objects can be imported. Objects of the `Appendable` and `Symlink` types are not supported.<br><br>* Creating DataFlow policies for TOS HNS buckets is not supported.<br><br>* DataFlow only supports Lazyload, importing, or exporting of data stored in TOS **Standard Storage**. All other TOS storage types, including Archive and Cold Archive, are incompatible with DataFlow operations. If a DataFlow policy is associated with a TOS bucket containing Archive or Cold Archive data, you must fully restore the archived data. Failure to do so will result in:<br><br>   * Errors when attempting to Lazyload archived data.<br><br>   * Failures to synchronize TOS data.<br><br>   * Additional charges for reading or writing TOS archived or cold archived data. |
|TOS versioning |EFS DataFlow is not affected by the versioning settings of the TOS bucket. |
|User\-defined metadata in TOS |DataFlow relies on the file system's extended attributes (`xattr`) and the [user-defined metadata](https://docs.byteplus.com/en/docs/tos/docs-managing-file-metadata) capability of TOS. TOS supports user\-defined metadata prefixed with `x-tos-meta-` for customized file management.<br><br><br>* By default, DataFlow uses the user\-defined metadata `x-tos-meta-anser_header`, which cannot be deleted or modified. Doing so may disrupt the normal operation of DataFlow.<br><br>* **TOS data update synchronization** or **import** tasks will not import any user\-defined metadata you have set in TOS.<br><br>* For **reverse synchronization of EFS to TOS** or **export** tasks, the extended attributes (`xattr`) customized in the file system will not be exported to TOS. |
|TOS event notifications |EFS lets you set up TOS event notifications based on trigger conditions. The supported event types are:<br><br><br>* tos:ObjectCreated:Put<br><br>* tos:ObjectCreated:Post<br><br>* tos:ObjectCreated:Origin<br><br>* tos:ObjectCreated:Fetch<br><br>* tos:ObjectCreated:Copy<br><br>* tos:ObjectCreated:CompleteUpload<br><br>* tos:ObjectReplication:ObjectCreated<br><br>* tos:ObjectReplication:ObjectModified<br><br>* tos:ObjectRemoved:Delete<br><br>* tos:ObjectRemoved:DeleteMarkerCreated<br><br>* tos:LifecycleExpiration:Delete<br><br>* tos:LifecycleExpiration:DeleteMarkerCreated<br><br><br>For more information, see [Event notification overview](https://docs.byteplus.com/en/docs/tos/Event-notification-overview). |
|Symbolic links and hard links |Exporting `hard links` and `symbolic links` to TOS buckets is not supported. |
|Constraints on renaming subdirectories in the file system path for the DataFlow policy |* The system call sys_rename is not supported and will return the error code EXDEV.<br><br>* Although you can rename subdirectories using the mv command, please note that the operation may incur significant latency depending on the number of files within the subdirectory. |
|Authorization |* EFS DataFlow requires access to TOS. Revoking this access will stop DataFlow.<br><br>* EFS log analysis requires access to Torch Log Service (TLS). Revoking this access will stop log analysis. |
|File conflict policy |If you select the policy of **Preserve** **Latest** **Files**, import and export tasks will skip files with the same name in both EFS and TOS that were modified at the same time (with second\-level precision). |
|Deleting file systems |If you delete a file system with a running Dataflow policy, the system will not automatically synchronize or export any newly added or modified files in the relevant paths to the associated TOS bucket. To do so, create a new export task and complete it before deleting the file system. |
|Stopping import rules |After you stop an import rule, wait 60 seconds before restarting it. |


<span id="PmKUbVvn"></span>
## Billing notes


* TOS will charge storage fees for data written to it. For billing details, see [Storage](https://docs.byteplus.com/en/docs/tos/docs-storage-fee).

* After log analysis is enabled, Torch Log Service (TLS) charges based on the actual volume of data written and other billable items. For billing details, see [TLS Billing overview](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode).
