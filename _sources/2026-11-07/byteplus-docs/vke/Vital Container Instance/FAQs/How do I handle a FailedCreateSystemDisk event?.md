---
title: "How do I handle a FailedCreateSystemDisk event?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-handle-a-FailedCreateSystemDisk-event"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

In VCI services that use image caching and have specified a system volume size, the following **FailedCreateSystemDisk** event occurs, resulting in pod creation failure:

```sql
FailedCreateSystemDisk
The size of specified system disk is too small to meet the requirements of the target image cache
```


<span id=".6Zeu6aKY5YiG5p6Q"></span>
## Problem analysis

This issue typically arises when the system volume size specified via the `vci.vke.volcengine.com/desired-system-storage` annotation is smaller than the size of the image cache.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

When specifying the system volume size, follow these guidelines:


* Automatic image cache matching: `Image size × (2 ~ 2.5)`. For example, if the image size selected for VCI creation is 20 GiB, you need to specify a system volume size of 40 GiB to 50 GiB.

* Manually specified image cache: `Image cache capacity + 20 GiB`. For example, if your image cache size is 60 GiB, you need to specify a system volume size of 80 GiB. Therefore, you can adjust the system volume size or choose not to use image caching when creating the pod. For details, see [Creating VCIs with automatic image caching](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Automatic-Image-Cache) and [Creating VCIs with manual image caching](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache).
