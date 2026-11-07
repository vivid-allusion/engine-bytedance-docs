---
title: "katalyst"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/katalyst"
---

The katalyst add\-on provides fine\-grained resource management capabilities, such as topology reporting in Remote Direct Memory Access (RDMA) scenarios and core binding in Non\-Uniform Memory Access (NUMA)\-aware scheduling. This topic describes the change history of the katalyst add\-on.

For more information about add\-ons and how to use them, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

> **tip**

> This add\-on is currently in **public beta**.

## October 2026

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.19 |* v1.26.10\-vke.13 ≤ Cluster version ≤ v1.36<br><br>* v1.24.15\-vke.13 ≤ Cluster version ≤ v1.26 |Being maintained |* The Overlap CPU QoS feature is supported.<br><br>* ConfigMap content is not overwritten during an upgrade. |None |

## August 2026

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.17 |v1.26.10\-vke.13 ≤ Cluster version ≤ v1.36 |Being maintained |Supports the memory compression feature. |None |

## July 2026

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.15 |* v1.28.15\-vke.32 ≤ Cluster version < v1.30<br><br>* v1.30.4\-vke.17 ≤ Cluster version < v1.32<br><br>* v1.32.3\-vke.14 ≤ Cluster version < v1.34<br><br>* v1.34.6\-vke.9 ≤ Cluster version < v1.36<br><br>* Cluster version ≥ v1.36.1\-vke.2 |Maintained |Supports the node amplification feature. |None |

## June 2026

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.14 |* v1.24.15\-vke.13 ≤ Cluster version < v1.26<br><br>* v1.26.10\-vke.13 ≤ Cluster version < v1.36 |Maintained |* Supports automatic detection of Cgroup v1 and Cgroup v2 nodes.<br><br>* Fixes an issue where some versions lacked a closed‑interval configuration for Kubernetes version compatibility. |None |

## July 2025

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.10 |* v1.24.15\-vke.13 ≤ Cluster version < v1.26<br><br>* Cluster version ≥ v1.26.10\-vke.13 |Maintained |The Identity and Access Management (IAM) authentication method of the add\-on is optimized. |None |

## April 2025

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.9 |* v1.24.15\-vke.13 ≤ Cluster version < v1.26<br><br>* Cluster version ≥ v1.26.10\-vke.13 |Maintained |* The issue where the add\-on fails to start after being upgraded from an earlier version is fixed.<br><br>* Fixed the issue where the number of data points queried from Vital Managed Service for Prometheus (VMP) by the intelligent Horizontal Pod Autoscaler (HPA) exceeded VMP's query limit. |After you upgrade the version from v0.3.5\-vke.5 to v0.5.x or later, you need to change the `topology-manager-policy` field of the kubelet parameter for the node pool associated with the add\-on to `none`, and synchronize the update to existing nodes. For detailed operations, refer to [FAQ](https://docs.byteplus.com/en/docs/vke/Handling_the_impact_after_Katalyst_add-on_upgrade). |

## December 2024

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.13\-vke.8 |* v1.24.15\-vke.13 ≤ Cluster version < v1.26<br><br>* Cluster version ≥ v1.26.10\-vke.13 |Maintained |The CPU Burst feature is supported. |None |

## May 2024

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.5\-vke.5 |* v1.24.15\-vke.13 ≤ Cluster version < v1.26<br><br>* v1.26.10\-vke.13 ≤ Cluster version < v1.28 |Maintained |Different features can be enabled based on scenarios. |None |
|v0.3.3\-vke.4 |* v1.24.15\-vke.13 ≤ Cluster version < v1.26<br><br>* v1.26.10\-vke.13 ≤ Cluster version < v1.28 |No longer maintained |* Kubernetes v1.26 is supported.<br><br>* The Peripheral Component Interconnect Express (PCIe) switch topologies of nodes can be reported. |None |

## December 2023

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.3\-vke.3 |v1.24.15\-vke.13 ≤ Cluster version < v1.26 |No longer maintained |The RDMA topology information of nodes can be reported. |None |

## September 2023

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.2\-vke.2 |v1.24.15\-vke.13 ≤ Cluster version < v1.26 |No longer maintained |The issue where the CustomNodeResource resource occasionally persists after a node is deleted is fixed. |None |

## August 2023

|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.0\-vke.1 |v1.24.15\-vke.13 ≤ Cluster version < v1.26 |No longer maintained |The katalyst add\-on is released for invitational beta testing for the first time. |None |
