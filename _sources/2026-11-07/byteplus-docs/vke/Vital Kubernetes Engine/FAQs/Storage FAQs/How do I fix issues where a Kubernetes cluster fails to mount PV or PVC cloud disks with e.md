---
title: "How do I fix issues where a Kubernetes cluster fails to mount PV or PVC cloud disks with existing data?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-if-I-cannot-mount-a-PV_PVC-volume-that-already-contains-data-to-a-Kubernetes-cluster"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The Kubernetes cluster cannot mount PV or PVC cloud disks that already contain data, with the "wrong fs type, bad option, bad superblock on /dev/vdc" error message.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Pods only support using raw disks (for example, vdc) and do not allow cloud disks that already have partitions configured.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* **Solution 1**: If the existing cloud disk contains data, create a new cloud disk and copy or migrate the data from the original disk to the new one for data security.

* **Solution 2**: If the existing cloud disk does not contain any data, delete the existing partitions and continue using the disk.
