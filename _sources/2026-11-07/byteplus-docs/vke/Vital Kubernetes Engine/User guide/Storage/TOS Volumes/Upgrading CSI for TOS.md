---
title: "Upgrading CSI for TOS"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Description_of_the_TOS_CSI_capability_upgrade"
---

Vital Kubernetes Engine (VKE) supports the csi\-fsx add\-on, which allows you to use PersistentVolumes based on Torch Object Storage (TOS) via FSX access for better performance and availability. This topic describes the upgrade from csi\-tos to csi\-fsx.

<span id="Y3c4QGBz"></span>
## Deprecation of csi\-tos

The csi\-tos add\-on for S3FS\-based access method will soon be discontinued. For details, see [[Product update] csi-tos add-on EOM](https://docs.byteplus.com/en/docs/vke/Product_changes_csi-tos_add-on_EOM).

<span id="mbdZp6lH"></span>
## csi\-fsx limits

csi\-fsx does not support VCI. To use TOS PVs on VCI, continue using the csi\-tos add\-on for S3FS\-based access. For more restrictions related to the FSX client, see [FSX overview](https://docs.byteplus.com/en/docs/tos/Overview).

<span id="ovSq8MOE"></span>
## csi\-fsx features

FSX is a unified file access client provided by  for unstructured data storage. It supports standard POSIX semantics. You can mount a file system to a Linux system by using the FSX client for easy access to data in the file system.


|**Type** |**FSX** |
|---|---|
|Operating system |Only Linux is supported. For usage restrictions and compatibility notes, see [FSX overview](https://docs.byteplus.com/en/docs/tos/Overview). |
|Access protocol |Self\-developed high\-performance file storage protocol |
|POSIX compatibility |Partially compatible. For more compatibility information, see [FSX overview](https://docs.byteplus.com/en/docs/tos/Overview). |
|Single\-client performance |* Read: 9 GB/s<br><br>* Write: 11 GB/s |
|Mount entry |Endpoint |
|Client hot upgrade |Supported |
|Enterprise features |Client\-side cache |


<span id="YXdNukr7"></span>
## Add\-on switching method

The csi\-tos and csi\-fsx add\-ons are independent of each other and have no dependencies. After installing the csi\-fsx add\-on in the cluster, you can use TOS PVs through FSX access.

Before uninstalling the csi\-tos add\-on, make sure that no new PVs that use the S3FS access method are added and that all existing PVs have been removed. Otherwise, existing TOS PVs and PVCs that use the S3FS access method will not function as expected.

<span id="d5NeEjUL"></span>
## csi\-fsx usage

You can use static TOS PVs by using the FSX client through the console or Kubectl command line. For more details, see [Accessing static TOS PVs by using the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).
