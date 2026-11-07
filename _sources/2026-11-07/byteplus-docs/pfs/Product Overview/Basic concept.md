---
title: "Basic concept"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Basic-concepts"
---

This article introduces the common concepts and explanations related to file system PFS.


|Concept #{style="width: 200px;"}# |Description |
|---|---|
|PFS |PFS is a high\-throughput, low\-latency, scalable parallel file system service that provides file storage services for high\-performance computing scenarios. |
|POSIX |Portable Operating System Interface POSIX (Portable Operating System Interface) is the collective name of a series of interrelated standards defined by IEEE for running software on various UNIX operating systems. Programs written for a POSIX\-compliant operating system can be compiled and executed on any other POSIX operating system. |
|Region |The physical location of the data center. When PFS meets cross\-regional access or hosts business systems in different regions, it needs to be configured on demand according to the region. Currently supported regions are as follows:<br><br><br>* ap\-southeast\-1 |
|Zone |Availability zones refer to independent physical areas in the same region where power and network are interconnected. |
|VPC |Private network VPC is a virtual private network, and VPCs are isolated from each other. |
|Mount Service |The mount service is the connection point for file systems in a network environment. The file system needs to be mounted on the computing node to complete data access and storage. Mounting is the operation of connecting a compute node to a file system. |
