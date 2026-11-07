---
title: "Access point overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Access_point_overview"
---

An access point provides directory\-level entry to file systems in BytePlus FileNAS. You can create multiple access points for each directory and configure access policies based on business needs. This enables you to manage permissions for different users on the same dataset in a fine\-grained manner.

<span id="923467b2"></span>
## Features


* Tenant isolation at directory level

   Each access point is linked to a root directory, which is a subdirectory of the file system. When you access the file system via the access point, you can only access the data within the corresponding root directory.

* Simplified permission management

   * Cache FileNAS allows you to manage permissions using IAM. You can set IAM policies for access points and grant access to different IAM users or roles.

   * Cache FileNAS uses a single POSIX identity for read and write actions when accessing the file system through an access point.


<span id="97ab8581"></span>
## Difference between an access point and a mount target

Access points and mount targets are different methods for resource access, each suitable for specific scenarios. Here are their key differences.


|**Parameters** ||**Access point** |**Mount target** |
|---|---|---|---|
|Client ||Self\-developed high\-performance file storage client FSX |NFS client |
|Access protocol ||Self\-developed file storage protocol |NFSv3, NFSv4.1, etc. |
|Export scope ||Directory level |File system level |
|Permission management |File system permission management |* Directory owner<br><br>   Modifies the owner information of an existing directory using chgrp.<br><br>* POSIX permissions<br><br>   Modifies the POSIX permissions of an existing directory using chmod.<br><br>* Access Control List (ACL)<br><br>   Allows the specified user (uid) or user group (gid) to have read, write, and execute access to the specified directory or file. |* Directory owner<br><br>   Modifies the owner information of an existing directory using chgrp.<br><br>* POSIX permissions<br><br>   Modifies the POSIX permissions of an existing directory using chmod.<br><br>* Access Control List (ACL)<br><br>   Allows the specified user (uid) or user group (gid) to have read, write, and execute access to the specified directory or file. |
||Permission group management |Access points can be associated with permission groups that limit file system access to certain IP addresses or ranges. After association, only clients that meet the group’s rules can access the access point. |Mount targets can be associated with permission groups that limit file system access to certain IP addresses or ranges. After association, only clients that meet the group's rules can access the mount target. |
||Access point permission management |* Directory owner<br><br>   Specifies directory ownership when created.<br><br>* POSIX permissions<br><br>   Specifies the POSIX permissions for new directories when created.<br><br>* Specifies POSIX user/user group<br><br>   All client\-side file operations through this access point will be mapped to the specified POSIX user/group ID.<br><br>* Access point policy<br><br>   Uses IAM policies to limit client access to the specific access point to certain accounts only Multiple access points can be created under the same file system directory; the same access point can configure different access permissions for different accounts. |None |


<span id="1a716743"></span>
## Usage limits


|**Limits** |**Value** |
|---|---|
|File storage type supported |Cache FileNAS |
|Number of access points that can be created in a single file system |1,000 |
|Maximum compute nodes per access point |1,000 |
|Maximum number of open files |1 million |
|Filename length limit |255 bytes |
|Maximum directory depth |Absolute path length no longer than 4096 |
