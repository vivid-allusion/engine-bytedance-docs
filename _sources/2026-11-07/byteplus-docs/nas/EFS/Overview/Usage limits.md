---
title: "Usage limits"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Usage_limits"
---

This topic describes the usage limits for Elastic File Storage (EFS).

<span id="rNrJ0gcG"></span>
## Access restrictions

EFS is currently in closed beta. To use EFS, contact your account manager for access.

<span id="t4mUNavi"></span>
## File system


|**Category** |**Description** |
|---|---|
|Number of file systems that can be created per account in a single region |20<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you need to create more than 20 file systems, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001576">submit a ticket</a> to apply.</div><br> |
|Maximum number of mount targets per file system |3 |
|Maximum number of files per file system |Defaults to 1 billion, Premium Tier file systems support up to 100 billion. |
|Maximum directory depth per file system |1,000 levels |
|Maximum capacity of a single file system |10 PiB |
|Maximum number of concurrent mounts per file system |1,000 |


<span id="FzzJCnLJ"></span>
## File


|**Category** |**Description** |
|---|---|
|Naming rules |The maximum filename length is 255 bytes. |
|Maximum size of a single file |64 TiB |
|Maximum number of hard links per file |511 |


<span id="CZSLhJ8l"></span>
## Permission group


|**Category** |**Description** |
|---|---|
|Number of permission groups that can be created per account in a single region |100<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you need to create more than 100 permission groups, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001576">submit a ticket</a> to apply.</div><br> |
|Maximum number of permission group rules per group |100 |


<span id="a5aeD2UH"></span>
## Client operating system


|**Category** |**Description** |
|---|---|
|Linux |EFS fully verifies operating system images for mount access clients. For optimal file system performance, we recommend that you use kernel images and newer versions. Client operating system types and kernel versions not on the compatibility list are not supported.<br><br><br>* For supported operating systems and kernel versions for NFS clients, see [Recommended NFS kernel versions](https://docs.byteplus.com/en/docs/nas/Recommended_NFS_kernel_versions).<br><br>* For supported operating systems and kernel versions for FSX clients, see [FSX Operating environment](https://docs.byteplus.com/en/docs/nas/efs_FSX_overview#vXm4BPZj). |
|macOS |Not supported. |
|Windows |Not supported. |
|AIX |Not supported. |


<span id="HCKgaEu3"></span>
## NFS protocol


|**Category** |**Description** |
|---|---|
|Protocol versions |When mounting file systems on Linux, both NFSv4.1 and NFSv3 are supported. |
|File permissions |The following features are not supported:<br><br><br>* POSIX SetUID<br><br>* SetGID<br><br>* Sticky Bits |
|NFSv4.1 features |* Delegation is not supported.<br><br>* Nconnect is not supported.<br><br>* ACL is not supported.<br><br>* RPCSEC\-GSS authentication is not supported. |
|NFSv4.1 attributes |The following attributes are not supported:<br><br><br>* FATTR4_MIMETYPE<br><br>* ATTR4_QUOTA_AVAIL_HARD<br><br>* FATTR4_QUOTA_AVAIL_SOFT<br><br>* FATTR4_QUOTA_USED<br><br>* FATTR4_TIME_BACKUP<br><br>* FATTR4_TIME_CREATE<br><br>* FATTR4_ARCHIVE<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you use these attributes, <code>/var/log/messages</code> will display an "NFS4ERR_ATTRNOTSUPP" error.</div><br> |
|NFSv4.1 commands |The following commands are not supported:<br><br><br>* OP_DELEGPURGE<br><br>* OP_DELEGRETURN<br><br>* NFS4_OP_OPENATTR<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you use these commands, <code>/var/log/messages</code> will display an "NFS4ERR_ATTRNOTSUPP" error.</div><br> |
|NFSv3 restrictions |* File locking is not supported.<br><br>* Nconnect is not supported.<br><br>* ACL is not supported. |
|NFS clients |* The maximum concurrent requests for a single NFS client is 128.<br><br>* The maximum read and write bandwidth for a single NFS client is 2~3 GB/s.<br><br>* An NFS client can open up to 32,768 files at the same time.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <code>list</code> directory and files under it are excluded from open file statistics.   </div><br>   <br><br>* An NFS client can acquire up to 8,192 locks across a maximum of 256 files or processes for each file system mounted. For instance, one process can hold one or more locks on up to 256 files. Eight processes can each hold one or more locks on up to 32 files.<br><br>* TCP Multi\-channel protocol is not supported for NFS client mounts. |


<span id="qMel8JDD"></span>
## Tag


|**Category** |**Description** |
|---|---|
|Quantity |A file system can have up to 50 tags. |
|Tag keys |If you want to add multiple tags to a file system, tag keys must be unique. |
|Region |Tag information is not shared across regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region. |
