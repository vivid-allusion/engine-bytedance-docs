---
title: "Limits"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Limits"
---

This topic covers the usage limitations of Extreme FileNAS and Cache FileNAS.

<span id="pQ46SYPR"></span>
## Extreme FileNAS


|**Category** |**Limits** |**Description** |
|---|---|---|
|File protocol |NFS file systems |* The maximum file name length is 255 bytes.<br><br>* Linux mount operations support exclusively NFSv3.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">NFSv4.0 or NFSv4.1 is incompatible with Extreme FileNAS.   </div><br>   <br><br>* The POSIX permission bits (SetUID, SetGID, and Sticky Bits) are not supported.<br><br>* An NFS client can open up to 32,768 files at the same time. Files within `list` directories are excluded from open file statistics.<br><br>* An NFS client can acquire up to 8,192 locks across a maximum of 256 files or processes for each file system mounted. For instance, one process can hold one or more locks on up to 256 files. Eight processes can each hold one or more locks on up to 32 files.<br><br>* For optimal NFS performance, we recommend using a non\-Windows operating system for client access. |
|Specification |Number of file systems that can be created per account in a single region |10 |
||Maximum number of mount targets per file system |3 |
||Maximum number of files per file system |1 billion |
||Maximum directory depth per file system |1000 levels |
||Maximum capacity of a single file system |64 TiB |
||Maximum number of concurrent mounts per file system |1,024 |
||Maximum size of a single file |64 TiB |
|Operating system |CentOS |Supported |
||Debian |Supported |
||Ubuntu |Supported |
|Usage |Regions and availability zones |Once the file system is created, the region and availability zone cannot be changed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For optimal performance, deploy your file system and compute nodes in the same availability zone.</div><br> |
||Mount targets |File systems are mounted on compute nodes via the Command Prompt. Requirements for mount targets:<br><br><br>* A single mount target in a network environment can be shared across hundreds of nodes, enabling collective access to the file system.<br><br>* The network type of the mount target must match that of the compute nodes. |
||Permission groups |A mount target must be bound to one and only one permission group. Requirements for permission groups:<br><br><br>* A single permission group can be bound to multiple mount targets.<br><br>* An account can have up to 100 permission groups.<br><br>* A permission group can have up to 100 rules. |
|Network |Virtual private cloud (VPC) |File systems must be deployed in the same VPC as business nodes. |


<span id="iSpfzCWc"></span>
## Cache FileNAS

<span id="alh2h6Rb"></span>
### File systems


|**Limits** |Value |
|---|---|
|Number of file systems that can be created per account in a single region |20<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The cluster security architecture reduces the minimum guaranteed bandwidth per file system to below 600 MB/s once you have created more than 20 file systems. The minimum guaranteed bandwidth per file system: <code>S = 600 (MB/s) × 20 / M</code>, where <code>M</code> = Total number of your file systems.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To prevent performance degradation, maintain a minimum average utilization of 5 TiB per file system if you have deployed over 50 file systems.</div><br> |
|Maximum number of mount targets per file system |3 |
|Maximum number of files per file system |1 billion |
|Maximum directory depth per file system |1000 levels |
|Maximum capacity of a single file system |10 PiB |
|Maximum number of concurrent mounts per file system |1,000 compute nodes |


<span id="cOSg22mn"></span>
### Files


|**Limits** |**Value** |
|---|---|
|Maximum filename length |255 bytes |
|Maximum size of a single file |16 TiB |
|Maximum number of hard links per file |511 |


<span id="aqU4Yvwm"></span>
### Permission groups


|**Limits** |**Value** |
|---|---|
|Number of permission groups that can be created per account in a single region |20 |
|Maximum number of permission group rules per group |30 |


<span id="4aYJpW1f"></span>
### Operating system


|**Category** |Constraints and limitations |
|---|---|
|Images |We have undergone thorough validation with specific operating system images. For optimal performance, use the recommended kernel images and their updated versions for Cache FileNAS. Using images not included in the recommended list may result in interruptions to Cache FileNAS. |
|Kernel version |We have identified kernel versions that may cause issues with Cache FileNAS and recommended versions that are compatible with it. Using unsupported kernel versions may result in interruptions to Cache FileNAS. To ensure uninterrupted service, we strongly recommend upgrading. We will notify you of newly identified kernel compatibility issues via email, site messages, SMS, and console announcements. Please ensure you have access to these channels and respond promptly to all notifications. For more information, see the [Mounting FAQ](https://docs.byteplus.com/en/docs/nas/Mounting-FAQ). |
|macOS |Not supported. |
|Windows |Not supported. |
|AIX |Not supported. |


<span id="SSHM95s0"></span>
### NFS protocol


|**Category** |Constraints and limitations |
|---|---|
|Protocol versions |Linux mount operations support exclusively NFSv4.1. NFSv3 is not supported. |
|File permissions |The following features are not supported:<br><br><br>* POSIX SetUID<br><br>* SetGID<br><br>* Sticky Bits |
|NFSv4.1 features |Delegation is not supported. |
|NFSv4.1 attributes |The following attributes are not supported:<br><br><br>* FATTR4_MIMETYPE<br><br>* ATTR4_QUOTA_AVAIL_HARD<br><br>* FATTR4_QUOTA_AVAIL_SOFT<br><br>* FATTR4_QUOTA_USED<br><br>* FATTR4_TIME_BACKUP<br><br>* FATTR4_TIME_CREATE<br><br>* FATTR4_ARCHIVE<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you use these attributes, an "NFS4ERR_ATTRNOTSUPP" error will appear in <code>/var/log/messages</code>.</div><br> |
|NFSv4.1 commands |The following commands are not supported:<br><br><br>* OP_DELEGPURGE<br><br>* OP_DELEGRETURN<br><br>* NFS4_OP_OPENATTR<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you use these commands, an "NS4ERR_ATTRNOTSUPP" error will appear in <code>/var/log/messages</code>.</div><br> |
|NFS clients |* One NFS client can handle up to 128 concurrent requests.<br><br>* The maximum read and write bandwidth for a single NFS client is 500 MB/s.<br><br>* An NFS client can open up to 32,768 files at the same time.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <code>list</code> directory and files under it are excluded from open file statistics.   </div><br>   <br><br>* An NFS client can acquire up to 8,192 locks across a maximum of 256 files or processes for each file system mounted. For instance, one process can hold one or more locks on up to 256 files. Eight processes can each hold one or more locks on up to 32 files.<br><br>* TCP Multi\-channel protocol is not supported for NFS client mounts. |


<span id="4cHV6J0h"></span>
### DataFlow


|**Category** |Constraints and limitations |
|---|---|
|Maximum number of DataFlow policies per file system |20 |
|Maximum number of DataFlow tasks per file system |20. Each policy executes a single task. |
|Maximum number of concurrent tasks per file system |20 |
|Maximum number of concurrent tasks per DataFlow policy |1 |
|Maximum paths per import or export task |20 |
|Object names |The following names will be considered invalid and will not be processed during import or export operations:<br><br><br>* Object names containing `./` structures.<br><br>* Object names containing `../` structures.<br><br>* Object names with multiple consecutive forward slashes (`/`).<br><br>* Object names ending with a single forward slash (`/`).<br><br>* **Folder** or **file names** exceeding 255 characters in length.<br><br>* Object names consisting solely of dots (`.`). For example, `a/b/c/...`. |
|Object size |* The maximum object size for exporting is 16 TiB.<br><br>* Files larger than 16 TiB cannot be exported to TOS. |
|File system paths |* You can only create DataFlow policies for empty directories.<br><br>* The path cannot exceed 8 directory levels.<br><br>* The length should be between 3 and 1024 characters.<br><br>* Nested file system paths across DataFlow policies are not supported. |
|TOS buckets/prefixes |Nested TOS prefixes across DataFlow policies are not supported. |
|TOS storage types |* Creating DataFlow policies for TOS HNS buckets is not supported.<br><br>* DataFlow only supports the on\-demand loading, importing, or exporting of data stored in Torch Object Storage (TOS) **Standard Storage**. All other TOS storage types, including Archive and Cold Archive, are incompatible with DataFlow operations. If a DataFlow policy is associated with a TOS bucket containing Archive or Cold Archive data, you must fully restore the archived data. Failure to do so will result in:<br><br>   * Errors when attempting to load archived data on demand.<br><br>   * Failures to synchronize TOS data.<br><br>   * Additional charges for reading or writing TOS archived or cold archived data. |
|TOS versioning |Cache FileNAS DataFlow is not affected by the versioning settings of the TOS bucket. |
|User\-defined metadata in TOS |DataFlow relies on the file system's extended attributes (xattr) and the [Managing File Metadata](https://docs.byteplus.com/en/docs/tos/docs-managing-file-metadata) of TOS. TOS supports user\-defined metadata prefixed `withx-tos-meta-` for customized file management.<br><br><br>* By default, DataFlow uses the user\-defined metadata `x-tos-meta-anser_header`, which cannot be deleted or modified. Doing so may disrupt the normal operation of DataFlow.<br><br>* **TOS data update synchronization** or **import** tasks will not import any user\-defined metadata you have set in TOS.<br><br>* For **reverse synchronization of NAS to TOS** or **export** tasks, the extended attributes (xattr) customized in the file system will not be exported to TOS. |
|TOS event notifications |Cache FileNAS lets you set up TOS event notifications based on trigger conditions. The supported event types are:<br><br><br>* tos:ObjectCreated:Put<br><br>* tos:ObjectCreated:Post<br><br>* tos:ObjectCreated:Origin<br><br>* tos:ObjectCreated:Fetch<br><br>* tos:ObjectCreated:Copy<br><br>* tos:ObjectCreated:CompleteUpload<br><br>* tos:ObjectReplication:ObjectCreated<br><br>* tos:ObjectReplication:ObjectModified<br><br>* tos:ObjectRemoved:Delete<br><br>* tos:ObjectRemoved:DeleteMarkerCreated<br><br>* tos:LifecycleExpiration:Delete<br><br>* tos:LifecycleExpiration:DeleteMarkerCreated<br><br><br>For more information, see [Event notification overview](https://docs.byteplus.com/en/docs/tos/Event-notification-overview). |
|Symbolic links and hard links |Exporting hard links and symbolic links to TOS buckets is not supported. |
|Constraints on renaming subdirectories in the file system path for the DataFlow policy |* The system call sys_rename is not supported and will return the error code EXDEV.<br><br>* Although you can rename subdirectories using the mv command, please note that the operation may incur significant latency depending on the number of files within the subdirectory. |
|Authorization |* DataFlow requires FileNAS access to TOS. Revoking this access will stop DataFlow.<br><br>* FileNAS log analysis requires access to Torch Log Service (TLS). Revoking this access will stop log analysis. |
|File conflict policy |If you select the policy of **Keep the latest documents up to date**, the import and export tasks will skip files with the same name in both FileNAS and TOS that were modified simultaneously with second\-level precision. |
|Eviction policies and tasks |The eviction rules skip files that have been modified in the file system but have not yet been synchronized to the TOS bucket. |
|Deleting DataFlow policies |Deleting a DataFlow policy will permanently erase all data in the associated file system path. This action is immediate and irreversible. |
|Deleting file systems |If you delete a file system with a running Dataflow policy, the system will not automatically synchronize or export any newly added or modified files in the relevant paths to the associated TOS bucket. To do so, create a new export task and complete it before deleting the file system. |
|Stopping export rules |Stop the import rule and wait 60 seconds before restarting it. |


<span id="3d4TCBTJ"></span>
### Tags


|Category |Constraints and limitations |
|---|---|
|Quantity |A file system can have up to 50 tags. |
|Tag keys |If you want to add multiple tags to a file system, tag keys must be unique. |
|Region |Tag information is not shared across regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region. |


&nbsp;
