---
title: "FSX overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/FSX_overview"
---

FSX is a unified file access client offered by BytePlus. It supports standard POSIX semantics and is compatible with unstructured data storage systems, including FileNAS, PFS, and TOS. To easily access and use the data in a file system, you can mount it to Linux using FSX.

<span id="75ccf9d1"></span>
## Operating environment 

Currently, FSX only works with the x86_64 architecture and is not compatible with Windows or macOS. See the table below for supported environments.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">FSX exclusively supports public images from BytePlus, and does not accommodate custom user images. </div>



|**Operating system** |**Version** |**Kernel version** |
|---|---|---|
|Debian |11 |5.10.0 |
|CentOS |8 |4.18.0 |
|CentOS Stream |8 |4.18.0 |
|Ubuntu |18.04 |4.15.0 |
||20.04 |5.4.0 |
||22.04 |5.15.0 |
|veLinux |1.0 |5.4.0 |
|||5.4.0 CentOS Compatible Version |
|||5.10.0 |
|||5.10.0 CentOS Compatible Edition |
||2.0 |5.15.0 |
|||5.15.0 CentOS Compatible Edition |


<span id="588e8ca7"></span>
## Differences between FSX and NFS 

FileNAS allows you to mount file systems using an FSX client or an NFS client. The following information highlights the differences between the two, helping you use FSX effectively.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">FSX accesses FileNAS, vePFS and TOS differently. The table below compares FSX with NFS on FileNAS.</div>



|**Category** |**FSX** |**NFS** |
|---|---|---|
|Supported FileNAS edition |Cache FileNAS |Cache FileNAS and Extreme FileNAS |
|Operating system |Linux only |Linux and Windows (Windows support is not recommended and is limited to NFSv3) |
|Access protocol |Self\-developed high\-performance file storage client |NFSv3 and NFSv4.1 |
|POSIX compliance |Fully compliant |Fully compliant |
|Single client throughput |8 GB/s |3 GB/s |
|Mount entry |Access point |Mount target |
|Hot upgrade |Supported |Not supported |


<span id="f3431048"></span>
## Usage limits


|Limits |Value |
|---|---|
|Supported file system edition |Cache FileNAS |
|Maximum file name length |255 bytes |


<span id="5906a96a"></span>
## Steps


1. Create an access point. For more information, see [Creating access points](https://docs.byteplus.com/en/docs/nas/Managing_access_points#a4a6cb20).

2. (Optional) Configure the access point policy. For more information, see [Configuring access point policies](https://docs.byteplus.com/en/docs/nas/Configuring_access_point_policies).

3. Install an FSX client. For more information, see [Installing FSX](https://docs.byteplus.com/en/docs/nas/Installing_FSX).

4. Obtain the mount command for the access point. For more information, see [Viewing access point mount commands](https://docs.byteplus.com/en/docs/nas/Viewing_access_point_mount_commands).

5. Mount the file system through the access point. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/Mounting_file_systems).
