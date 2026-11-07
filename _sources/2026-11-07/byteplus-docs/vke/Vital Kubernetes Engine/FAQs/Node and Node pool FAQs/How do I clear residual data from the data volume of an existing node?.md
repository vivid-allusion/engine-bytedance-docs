---
title: "How do I clear residual data from the data volume of an existing node?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-clean-up-residual-data-on-the-data-volumes-of-existing-nodes"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

After you add an ECS instance attached with a data volume as **an existing node** to a VKE cluster, you need to clear the data volume in advance if you need to mount the data volume on the `/var/lib/containerd` and `/var/lib/kubelet` directories.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

This topic provides an example of how to clear `/dev/vdb`.


1. View the list of mounted file systems and confirm whether `/dev/vdb` is already mounted to a file system.

   ```bash
   df -h
   ```
   

2. Back up important data in `/dev/vdb` as needed.

3. After confirming that all processes that use the `/dev/vdb` directory have stopped, unmount `/dev/vdb`.

   ```bash
   umount /dev/vdb
   ```
   

1. Format `/dev/vdb`.

   ```bash
   mkfs.ext4 /dev/vdb
   ```
   

   The expected result is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d6e946c7a308e47b394bd498048baa95.png) </span>

1. Mount `/dev/vdb` again.

   ```bash
   mount /dev/vdb /mnt/vdb
   ```
   

6. Check whether the device is mounted.

   ```bash
   df -h
   ```
   

   The expected result is as follows: The corresponding ECS instance can be added as an existing node to the VKE cluster.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c467d619325fba05cf36caef2cd12eb.png) </span>
