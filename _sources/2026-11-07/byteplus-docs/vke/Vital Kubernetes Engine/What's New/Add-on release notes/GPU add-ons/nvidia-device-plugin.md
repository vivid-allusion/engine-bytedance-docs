---
title: "nvidia-device-plugin"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin"
---

nvidia\-device\-plugin is an NVIDIA GPU device management add\-on that supports using GPU devices inside containers. This topic describes the change history of the nvidia\-device\-plugin add\-on.

For more information about the add\-on and how to use it, see [nvidia-device-plugin](https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin-add-on?lang=en).

## October 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.2.0 |Cluster version: v1.24 or later |Being maintained |* You can specify a custom metric collection port for dcgm\-exporter (default: 9400).<br><br>* The HostNetwork mode can be enabled (disabled by default).<br><br>* You can configure CPU/memory requests and limits for device\-plugin and dcgm\-exporter. No limits are set by default. |None |

## July 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.0.0 |Cluster version: v1.24 or later |Being maintained |Upgrades nvidia\-device\-plugin to v0.19.2. |None |

## June 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.2.2 |Cluster version: v1.24 or later |Being maintained |Optimized the health check cycle to prevent the thundering herd effect. |None |

## May 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.2.1 |Cluster version: v1.24 or later |Being maintained |* Added the health check feature (with an interval of 8 minutes) to prevent nodes from reporting zero GPU resources when the gRPC connection between the device plugin and kubelet is interrupted.<br><br>* Adapted to cgroup v2 scenarios to prevent business containers from being unauthorized to access the device after systemctl daemon reload. |None |

## February 2026

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.2.0 |v1.20 ≤ Cluster version < v1.30 |Being maintained |* The XID health check feature is disabled by default.<br><br>* XID health checks ignore XID 109.<br><br>* PCIE topology reporting frequencies are reduced.<br><br>* dcgm\-exporter is upgraded to v4.2.3\-4.2.0.<br><br>* dcgm\-exporter supports configuring the collection interval, with the default value of 30 seconds.<br><br>* Changes to the dcgm\-exporter metrics:<br><br>   * The following metrics are deprecated: `DCGM_CUSTOM_XID_ERRORS_COUNTER` and `DCGM_CUSTOM_XID_ERRORS_TOTAL_COUNTER`.<br><br>   * The following metric is added: `DCGM_EXP_XID_ERRORS_COUNT`. |* After an XID error occurs, GPU scheduling will not be prohibited by default.<br><br>* If you are using the `DCGM_CUSTOM_XID_ERRORS_COUNTER` and `DCGM_CUSTOM_XID_ERRORS_TOTAL_COUNTER` metrics, switch to the `DCGM_EXP_XID_ERRORS_COUNT` metric. |

## August 2024

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.1.4 |v1.20 ≤ Cluster version < v1.30 |Being maintained |DCGM Exporter adds NVLINK metrics. |None |

## March 2024

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.1.3 |v1.20 ≤ Cluster version < v1.30 |Being maintained |* Supports turning off XID health check.<br><br>* Supports reporting the PCIE switch topology of GPU cards.<br><br>* Upgraded nvidia\-device\-plugin to v0.14.4. |None |

## December 2023

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.1.2 |v1.20 ≤ Cluster version < v1.30 |Being maintained |Fixed the issue of add\-on status anomaly when deleting a node pool. |None |

## October 2023

|**Version** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.1.1 |v1.20 ≤ Cluster version < v1.30 |Being maintained |Added metrics to DCGM Exporter. |None |

## April 2023

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.7 |v1.20 ≤ Cluster version < v1.30 |Being maintained |Upgrade nvidia\-device\-plugin container image to community version v0.13.0. |None |

## December 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.6 |v1.20 ≤ Cluster version < v1.30 |Being maintained |The add\-on architecture is optimized. |None |
|v1.0.5 |v1.20 ≤ Cluster version < v1.30 |No longer maintained |Adjust deviceIDStrategy to index. |None |

## November 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.4 |v1.20 ≤ Cluster version < v1.30 |No longer maintained |Supports custom installation of NVIDIA GPU resource monitoring plugin dcgm\-exporter. |None |

## September 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.3 |v1.20 ≤ Cluster version < v1.30 |No longer maintained |The add\-on architecture is optimized. |None |

## February 2022

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.2 |v1.20 ≤ Cluster version < v1.30 |No longer maintained |Added support for Tesla\-T4 and Tesla\-V100 graphics card types. |None |

## December 2021

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.1 |v1.20 ≤ Cluster version < v1.30 |No longer maintained |Optimize supported GPU node specifications (ECS type). |None |
|v1.0.0 |v1.20 ≤ Cluster version < v1.30 |No longer maintained |Initial release of the nvidia\-device\-plugin add\-on. |None |
