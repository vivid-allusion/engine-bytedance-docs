---
title: "mgpu"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/mgpu"
---

The mgpu add\-on is a shared GPU add\-on provided by Vital Kubernetes Engine (VKE). It enables multiple containers to share GPU cards by isolating video memory and compute resources across containers. This topic describes the change history of the mgpu add\-on.

For more information about the add\-on and how to use it, see [mgpu](https://docs.byteplus.com/en/docs/vke/mgpu-add-on?lang=en).

## September 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.8.3 |v1.24 ≤ Cluster version ≤ v1.36 |Being maintained |* Add\-on observability metrics are added.<br><br>* Hot upgrade defects are fixed.<br><br>* Metadata access can be based on a PrivateLink endpoint. |None |

## July 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.8.2 |v1.24 ≤ Cluster version ≤ v1.36 |Being maintained |Supports velinux2. |None |

## June 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.8.0 |v1.32 ≤ Cluster version ≤ v1.36 |Being maintained |* Fixed compatibility issues with systemd cgroup.<br><br>* Fixed cross\-process GPU memory usage statistics issues. |None |

## April 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.7.0 |v1.32 ≤ Cluster version ≤ v1.36 |Being maintained |* Adapted to containerd 2.x version.<br><br>* Supported the hot upgrade of the mgpu driver. |None |

## October 2025

|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.6.6 |v1.20 ≤ Cluster version ≤ v1.32 |Being maintained |* Supported DKMS.<br><br>* Supported Vulkan. |None |

## June 2025

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.6.5 |All versions |Being maintained |A Pod liveness probe can be configured. |None |

## April 2025

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.6.4 |All versions |Being maintained |Optimized cgroup collection logic in exporter. |None |

## March 2025

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.6.3 |All versions |Being maintained |Fixed the issue where a single container application requested mGPU memory exceeding 400G. |None |
|v0.6.2 |All versions |Being maintained |* exporter upgrades DCGM version.<br><br>* exporter supports configuring the collection interval. |None |

## February 2025

|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.6.1 |All versions |Being maintained |Supports large memory specifications such as H20 models. |None |
|v0.6.0 |All versions |Being maintained |Supports online\-offline hybrid deployment. |None |

## September 2024

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.5.1 |All versions |Being maintained |Converges unnecessary ServiceAccount permissions. |None |

## March 2024

|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.5.0 |All versions |Being maintained |When Pod exclusively occupies the whole card, the card\-level metrics add 3 labels, including pod, namespace, and container. |None |

## November 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.4.2 |All versions |Being maintained |The `mem_copy_util` metric is supported. |None |

## September 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.4.1 |All versions |Being maintained |Optimizes exporter listening resource logic. |None |

## August 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.4.0 |All versions |Being maintained |Standardization of add\-on parameter naming. |None |

## June 2023

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.0 |All versions |Being maintained |* Supports outputting mgpu version label to nodes.<br><br>* Integrates the mGPU driver installation feature, allowing users to optionally install mGPU drivers. |* The user\-created node pool scenario must upgrade its version to v0.3.0 to properly install the mGPU driver and use the mGPU feature.<br><br>* The stock GPU node pools can be used properly without configuration changes or refreshing initialization scripts. Scale\-out nodes are not affected. |

## March 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.0 |All versions |No longer maintained |Supports multi\-card sharing and matching monitoring. |None |

## January 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.1 |All versions |No longer maintained |Supports mgpu\-driver health check. |None |

## November 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.0.3 |All versions |No longer maintained |* Allows customized installation of shared GPU resources monitoring plugin mgpu\-exporter.<br><br>* Supports configuring computing power allocation policy QoS Policy. |None |

## October 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.0.2 |All versions |No longer maintained |Optimizes the scheduling relationship between the mGPU add\-on and non\-GPU nodes. |None |

## September 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.0.1 |All versions |No longer maintained |mGPU add\-on releases the first beta. |None |
