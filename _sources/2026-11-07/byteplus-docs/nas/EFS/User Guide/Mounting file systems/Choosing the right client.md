---
title: "Choosing the right client"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Choosing_the_right_client"
---

FSX is a unified file access client offered by BytePlus. It supports standard POSIX semantics and is compatible with unstructured data storage systems, including EFS, vePFS, and TOS. To easily access and use the data in a file system, you can mount it to Linux using FSX.

<span id="Hvr2Wz5r"></span>
## Supported clients for EFS

For a description of FSX, see [FSX overview](https://docs.byteplus.com/en/docs/nas/efs_FSX_overview).


|**Category** |**FSX** |**NFS** |
|---|---|---|
|Recommended scenarios |* When NFS single\-client performance cannot meet your business requirements<br><br>* When your business operations rely on directory\-level access control<br><br>* When you need to accelerate client\-side caching |* When NFS single\-client performance meets your business requirements<br><br>* When your client is not compatible with FSX |
|Operating system |Only Linux is supported. For compatibility details, see the Operating environment section below. |Linux and Windows (Windows only supports NFSv3 and is not recommended) |
|Access protocol |Self\-developed high\-performance file storage client |NFSv3 and NFSv4.1 |
|POSIX compliance |Fully compliant |Fully compliant |
|Single\-client throughput |10 GB/s |2–3 GB/s |
|Single\-client caching |45 GB/s (closed beta) |Not supported |
|Mount entry |Access point |Mount target |
|Hot upgrade |Supported |Not supported |
|Other features |* Directory\-level access control based on Identity and Access Management (IAM)<br><br>* Client\-side caching |Not supported |


<span id="cOwsN3ds"></span>
## Supported clients for TOS

For a description of FSX, see [FSX overview](https://docs.byteplus.com/en/docs/tos/Overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">This topic is only relevant in scenarios where you want to mount to compute nodes via POSIX.</div>



|**Category** |**FSX** |
|---|---|
|Operating system |Only Linux is supported. For compatibility details, see the Operating environment section below. |
|Access protocol |Self\-developed high\-performance file storage client |
|POSIX compliance |Partially compliant. For compliance details, see [FSX overview](https://docs.byteplus.com/en/docs/tos/Overview) |
|Single\-client throughput |* Read: 9 GB/s<br><br>* Write: 11 GB/s |
|Single\-client caching |45 GB/s (closed beta) |
|Mount entry |Endpoint |
|Hot upgrade |Supported |
|Other features |Client\-side caching |


<span id="detBU698"></span>
## Supported clients for FileNAS

Extreme FileNAS and Capacity FileNAS only support the NFS protocol.


|**Category** |**NFS** |
|---|---|
|Recommended scenarios |All scenarios |
|Operating system |Linux and Windows (Windows only supports NFSv3 and is not recommended) |
|Access protocol |* Extreme FileNAS: NFSv3<br><br>* Capacity FileNAS: NFSv4.1 and NFSv3 |
|POSIX compliance |Fully compliant |
|Single\-client throughput |2–3 GB/s |
|Single\-client caching |Not supported |
|Mount entry |Mount target |
|Hot upgrade |Not supported |
|Other features |Not supported |


<span id="GJtg9kNe"></span>
## Operating environment

Currently, FSX only works with the x86_64 architecture and is not compatible with Windows or macOS. See the table below for supported environments.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">FSX exclusively supports public images from BytePlus, and does not accommodate custom user images. If your environment is not listed below, you can <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001576">submit a ticket</a> to reach us.</div>



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
||Rocky Linux 9.1 |* 5.14.0\-284.30.1.el9_2.x86_64<br><br>* 5.14.0\-362.13.1.el9_3.x86_64 |
||Rocky Linux 9.2 ||
||Rocky Linux 9.3 ||
||Rocky Linux 9.4 ||
||Rocky Linux 9.5 |5.14.0\-503.26.1.el9_5 |


<span id="rD3G68po"></span>
##
