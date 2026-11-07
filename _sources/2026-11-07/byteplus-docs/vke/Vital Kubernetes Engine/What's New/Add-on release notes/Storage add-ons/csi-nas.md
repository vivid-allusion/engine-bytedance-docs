---
title: "csi-nas"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-nas"
---

The csi\-nas add\-on is a FileNAS service add\-on that provides the standard CSI interface, enabling container clusters to use the File Storage service. This topic describes the change history of the csi\-nas add\-on.

For more information about the add\-on and how to use it, see [csi-nas](https://docs.byteplus.com/en/docs/vke/csi-nas-add-on).

## September 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.4.0 |All versions |Being maintained |Metric collection is supported. |None |

## March 2026

|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.2 |All versions |Being maintained |The WatchList feature is enabled by default to optimize APIServer memory usage. For details, see [Streaming List responses](https://kubernetes.io/blog/2025/05/09/kubernetes-v1-33-streaming-list-responses/). |Slightly increases client\-side processing duration. |

## February 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.1 |All versions |Being maintained |Synchronizes with the latest community version to resolve known CVE issues. |None |

## December 2025

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.0 |All versions |Being maintained |* Added support for modifying the port for node CSI health checking. The default is 9908.<br><br>* Added support for modifying the Resources configuration of the node CSI container.<br><br>* Optimized speed of concurrent creation and deletion on a single host. |Node resource usage will increase, as the resource limits of the csi\-nas\-node container have been increased (from the default 200m1Gi to 4C4Gi) to optimize the speed of concurrent creation and deletion on a single host.  |

## May 2025

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.8 |All versions |Being maintained |Fixed the issue of taint configuration anomaly. |None |

## November 2024

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.7 |All versions |Being maintained |Fixed an issue where the permissions of dynamic\-volume subdirectories were not set to `777` when deployed in VCI mode. |None |

## October 2024

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.6 |All versions |Being maintained |Supports configuration of NodeSelector, Tolerations, and Resources for csi\-nas\-controller when installing add\-on. |None |

## September 2024

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.5 |All versions |Being maintained |* Fixed the issue where restarting ECS caused Pod to be Terminating.<br><br>* Fixed an issue where the directory was not actually mounted but the corresponding RPC unexpectedly returned success. |None |

## March 2024

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.3 |All versions |Being maintained |* Fixed the issue where Force Umount caused other local mount points to become unavailable when mounting the same remote NAS.<br><br>* Adjusted the memory limit of the CSI node to 1Gi. |None |

## February 2024

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.2 |All versions |Being maintained |Removed the dependency on the metadata server. |None |

## January 2024

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.1 |All versions |Being maintained |Avoids scheduling the add\-on pods to the DCP registered nodes. |None |
|v1.2.0 |All versions |Being maintained |Supports deployment on Vital Container Instance (VCI). |None |

## May 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.0 |All versions |Being maintained |Optimized the coding standards of the add\-on and upgraded the add\-on version. |None |

## March 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.4 |All versions |Being maintained |Supports the capacity\-type FileNAS. |None |
|v1.0.3 |All versions |Being maintained |The Vital Container Instance (VCI) deployment mode is supported. |None |

## December 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.2 |All versions |No longer maintained |Adapted to the Addon (add\-on) refactoring. |None |
|v1.0.1 |All versions |No longer maintained |Supports topology spread configuration. |None |

## November 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.0 |All versions |No longer maintained |Kubernetes v1.24 is supported. |None |

## September 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.3 |All versions |No longer maintained |Adapted the archiveOnDelete parameter in StorageClass, which lets users decide whether to archive NAS file data when deleting a StorageClass and reduces the risk of accidental data deletion. For related instructions on archiveOnDelete, refer to [Using NAS dynamic persistent volume](https://docs.byteplus.com/en/docs/vke/Using-dynamic-NAS-Volumes). |None |
