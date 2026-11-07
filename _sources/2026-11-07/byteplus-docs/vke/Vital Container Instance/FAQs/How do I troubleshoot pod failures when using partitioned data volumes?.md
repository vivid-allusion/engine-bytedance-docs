---
title: "How do I troubleshoot pod failures when using partitioned data volumes?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-troubleshoot-pod-failures-when-using-partitioned-data-volumes"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

When a partitioned data volume is mounted to a VCI pod, the VCI pod cannot run normally.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

VCI does not support partitioned data volumes. When using `fdisk` commands to partition a disk, do not create two or more partitions on the disk. Use a disk with only a single partition or a disk that has not been initialized as a data volume for the VCI pod.
