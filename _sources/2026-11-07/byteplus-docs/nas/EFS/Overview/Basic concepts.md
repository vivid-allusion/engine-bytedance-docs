---
title: "Basic concepts"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Basic_concepts"
---

This topic introduces the basic concepts related to Elastic File Storage (EFS).

<span id="Q0CS5ZZ7"></span>
## BytePlus general terminology


|Term |Description |
|---|---|
|Region |The region refers to the geographic area where physical data center is located. Usually, regions are classified by the city of the data center. Once the EFS file system is created, its region can not be changed. |
|Availability zone |An availability zone is a physically separate area within the same region, with independent power and networking. |
|[Private network](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) |The Virtual Private Cloud (VPC) creates an isolated, self\-configurable virtual network environment for cloud resources. |
|[Machine learning platform](https://docs.byteplus.com/en/docs/mlp/What_is_a_machine_learning_platform) |The Machine Learning Platform (MLP) is an enterprise\-level cloud\-native machine learning platform designed for machine learning application developers. It provides a variety of modeling and debugging tools such as development machines, custom tasks, and experiment management, as well as high\-performance inference services supporting multiple frameworks. |
|[Container service](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Kubernetes-Engine) |Container service Vital Kubernetes Engine (VKE) delivers enterprise\-level container management capabilities with high performance, reliability, and exceptional scalability. |


<span id="jgkT1Qrn"></span>
## File storage general terminology


|Term |Description |
|---|---|
|POSIX |Portable Operating System Interface (POSIX) is a set of standard interfaces defined to enable software to run on various Unix operating systems. Programs written for a POSIX\-compliant operating system can be compiled and executed on any other POSIX operating system. |
|Network File System (NFS) |Network File System (NFS) is the most widely used network file system for Linux or Unix environments. It supports standard POSIX semantics. |
|File system |A file system is a storage solution that manages files through a directory tree structure. It is categorized into local and remote file systems. Here, it refers specifically to remote file systems, which support concurrent access by multiple computing nodes and enable data sharing. |
|Bandwidth |Bandwidth refers to the amount of data that a file system can transfer within a specific time period. It usually measured in MB/s (megabytes per second) or GB/s (gigabytes per second). Bandwidth reflects the file system’s ability to handle continuous large file read and write operations. |
|Latency |Latency refers to the time interval from initiating a file operation request to completing the operation and receiving a response. The latency is usually measured in milliseconds (ms) or microseconds (μs). It reflects the responsiveness of the file system. |
|IOPS |IOPS (Input/Output Operations Per Second): The number of read and write operations that file system can perform per second (including read, write, and metadata queries). It is measured in ops/sec. It reflects the system's ability to process random small file read and write operations. |
|Metadata OPS |Metadata Operations Per Second (OPS) is a performance metric that measures how many metadata operations a file system can process per second. It measured in operations/second. These actions include file and directory creation, deletion, renaming, permission changes, attribute queries, and directory listings. |
|Capacity |Capacity refers to the total storage capacity of the file system. It is measured in units like GiB, TiB, or PiB.<br><br>The key difference between GB (Gigabyte) and GiB (Gibibyte) is the conversion base:<br><br><br>* GB: Based on the decimal system (powers of 10). 1GB = 10³ MB = 10⁶ KB = 10⁹ bytes (i.e., 1,000,000,000 bytes).<br><br>* GiB: Based on the binary system (powers of 2). 1GiB = 2<sup>10 </sup>MiB = 2<sup>20</sup> KiB = 2<sup>30</sup> bytes (i.e., 1,073,741,824 bytes). |


<span id="Oil2WW9P"></span>
## EFS specific terminology


|Term |Description |
|---|---|
|[EFS](https://docs.byteplus.com/en/docs/nas/What_is_Elastic_File_Storage) |Elastic File Storage (EFS) is a distributed file storage service provided by BytePlus. It offers scalable, high\-performance, and highly reliable storage. |
|[FSX](https://docs.byteplus.com/en/docs/nas/efs_FSX_overview) |FSX is a unified file access client offered by BytePlus. It supports standard POSIX semantics and is compatible with unstructured data storage systems, including EFS, PFS, and TOS. |
|Mount |Mounting connects compute nodes to the EFS file system. The EFS file system must be mounted to compute nodes before accessing and storing data. |
|[Mount target](https://docs.byteplus.com/en/docs/nas/efs_Managing_mount_targets) |Mount target is the connection point of the EFS file system in a network environment. |
|[Access point](https://docs.byteplus.com/en/docs/nas/efs_Access_point_overview) |The access point is the directory\-level access entry provided by EFS for the file system. |
|[Baseline Bandwidth mode](https://docs.byteplus.com/en/docs/nas/Managing_bandwidth_modes) |Baseline bandwidth mode is the default performance configuration for EFS. In this mode, file system performance grows linearly with capacity until reaching the maximum baseline bandwidth. |
|[Provisioned Bandwidth mode](https://docs.byteplus.com/en/docs/nas/Managing_bandwidth_modes) |The provisioned bandwidth mode is an additional performance configuration capability provided by EFS based on its capacity elasticity scaling capability. It can decouple the capacity and performance of a file system. |
|[Burst Bandwidth](https://docs.byteplus.com/en/docs/nas/efs_Managing_burst_bandwidth) |If workloads temporarily require higher performance beyond baseline and provisioned bandwidth, you can enable burst bandwidth to obtain additional bandwidth for a limited time. |
|[Permission group](https://docs.byteplus.com/en/docs/nas/efs_Managing_permission_groups) |Permission groups enable you to manage file system permissions via various mount targets. This includes authorizing IP addresses and granting read and write access. |
|[Directory quota](https://docs.byteplus.com/en/docs/nas/efs_Managing_directory_quotas) |Directory quotas are used to manage the capacity and file count within a specified directory. Two types are supported: statistical and restricted. |
