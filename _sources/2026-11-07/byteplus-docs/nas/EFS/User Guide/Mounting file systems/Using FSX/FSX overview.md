---
title: "FSX overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_FSX_overview"
---

FSX is a unified file access client offered by BytePlus. It supports standard POSIX semantics and is compatible with unstructured data storage systems, including EFS, vePFS, and TOS. To easily access and use the data in a file system, you can mount it to Linux using FSX.

<span id="vXm4BPZj"></span>
## Operating environment

Currently, FSX only works with the x86_64 architecture and is not compatible with Windows or macOS. See the table below for supported environments.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">FSX exclusively supports public images from BytePlus, and does not accommodate custom user images. If your environment isn't listed below, you can <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001576">submit a ticket</a> to reach us.</div>



|**Operating system** |**Version** |**Kernel version** |
|---|---|---|
|veLinux<br><br> |veLinux 1.0 |5.4.0 |
||veLinux 1.0 Centos compatible version |5.4.0 |
||veLinux 1.0 with 5.10 kernel |5.10.0 |
||veLinux 1.0 Centos compatible version with 5.10 kernel |5.10.0 |
||veLinux 2.0 |5.15.0 |
||veLinux 2.0 Centos compatible version |5.15.0 |
||Debian 12 |6.1.0\-18\-amd64 |
||Debian 11 |5.10.0\-30\-amd64 |
|||* 4.19.0\-26\-amd64<br><br>* 4.19.0\-27\-amd64 |
|||5.14.0\-312.el9.x86_64 |
|||* 4.18.0\-521.el8.x86_64<br><br>* 4.18.0\-553.5.1.el8.x86_64<br><br>* 4.18.0\-553.6.1.el8.x86_64 |
||CentOS 8.3 |4.18.0\-348.7.1.el8_5.x86_64 |
|||3.10.0\-1160.119.1.el7.x86_64 |
||CentOS 7.6 ||
||CentOS 7.3 ||
||CentOS 7.2 ||
||CentOS 7.1 ||
|Ubuntu |Ubuntu 24.04 |* 6.8.0\-36\-generic<br><br>* 6.8.0\-55\-generic |
||Ubuntu 24.04 with LLM Knowledge Base 64 bit |6.8.0\-36\-generic |
||Ubuntu 22.04 |* 5.15.0\-72\-generic<br><br>* 5.15.0\-91\-generic<br><br>* 5.15.0\-100\-generic<br><br>* 5.15.0\-124\-generic |
||Ubuntu 20.04 |* 5.4.0\-149\-generic<br><br>* 5.4.0\-186\-generic<br><br>* 5.4.0\-200\-generic |
||Ubuntu 18.04 |* 4.15.0\-211\-generic<br><br>* 4.15.0\-213\-generic |
|Rocky |Rocky Linux 8.6 |4.18.0\-553.5.1.el8_10.x86_64 |
||Rocky Linux 8.8 |4.18.0\-553.el8_10.x86_64 |
||Rocky Linux 9.1 |5.14.0\-284.30.1.el9_2.x86_64 |
||Rocky Linux 9.2 ||
||Rocky Linux 9.3 ||
||Rocky Linux 9.4 ||
||Rocky Linux 9.5 |5.14.0\-503.26.1.el9_5 |


<span id="JWEoSUUz"></span>
## Differences between FSX and NFS

EFS allows you to mount file systems using an FSX client or an NFS client. The following information highlights the differences between the two, helping you use FSX effectively.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">FSX accesses EFS and TOS differently. The table below compares FSX with NFS on EFS.</div>



|**Category** |**FSX** |**NFS** |
|---|---|---|
|Operating system |Linux only |Linux and Windows (Windows only supports NFSv3 and is not recommended) |
|Access protocol |Self\-developed high\-performance file storage client |NFSv3 and NFSv4.1 |
|POSIX compliance |Fully compliant |Fully compliant |
|Single\-client throughput |10 GB/s |2–3 GB/s |
|Mount entry |Access point |Mount targets |
|Hot upgrade |Supported |Not supported |


<span id="K0WB9pCP"></span>
## Usage limits


|Limit |Value |
|---|---|
|Maximum filename length |255 bytes |


<span id="sbQWZy10"></span>
## Workflow


1. Create an access point. For more information, see [Creating an access point](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#8DplUcqW).

2. (Optional) Configure the access point policy. For more information, see [Configuring access point policies](https://docs.byteplus.com/en/docs/nas/efs_Configuring_access_point_policies).

3. Install an FSX client. For more information, see [Installing FSX](https://docs.byteplus.com/en/docs/nas/efs_Installing_FSX).

4. Obtain the mount command for the access point. For more information, see [Viewing access point mount commands](https://docs.byteplus.com/en/docs/nas/efs_Viewing_access_point_mount_commands).

5. Mount the file system through the access point. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX).
