---
title: "cluster-autoscaler"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/cluster-autoscaler"
---

The cluster\-autoscaler add\-on automatically scales cluster nodes. It is a system\-managed tool that avoids user\-caused faults and poor performance, reducing your maintenance costs and improving stability. This topic describes the change history of cluster\-autoscaler.

For more information about add\-ons and how to use them, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* The cluster\-autoscaler add\-on has different version numbers on different Kubernetes versions. View add\-on upgrade records on the corresponding Kubernetes version as needed.

* The unmanaged cluster\-autoscaler add\-on is no longer supported. If you need to upgrade add\-on performance, uninstall the unmanaged add\-on and reinstall the latest version of the managed cluster\-autoscaler add\-on.


<span id=".a3ViZXJuZXRlcy12MS0zMi3lj5jmm7TorrDlvZU="></span>
## Change record

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Starting from v1.30.3\-vke.5, the cluster\-autoscaler add\-on is compatible with multiple Kubernetes versions and no longer needs a separate add\-on release for each Kubernetes version.</div>


<span id="0Car0rSR"></span>
### June 2026


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.11 |Cluster version ≥ v1.30 |Being maintained |System\-managed |Node scale\-out performance is optimized. |None |


<span id="9yLwQDzT"></span>
### January 2026


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.10 |Cluster version ≥ v1.30 |No longer maintained |System\-managed |* Supports configuring the maximum timeout duration for node readiness waiting.<br><br>* Supports configuring scale\-down delay calculation based on the local status of node pools.<br><br>* Supports ignoring resource usage of DaemonSet pods when calculating node scale\-down thresholds. |None |


<span id="xrYT2MpG"></span>
### November 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.9 |Cluster version ≥ v1.30 |Being maintained |System\-managed |* Optimize stability of self\-healing from abnormal node scaling.<br><br>* Optimize node scaling performance for large\-scale clusters. |None |


<span id="sFWL8Wmq"></span>
### October 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.8 |v1.30 ≤ cluster version ≤ v1.32 |No longer maintained |System\-managed |Optimize node scaling stability in CSI scenarios. |None |


<span id="_2025-06"></span>
### June 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.5 |v1.30 ≤ cluster version ≤ v1.32 |No longer maintained |System\-managed |Compatible with Kubernetes Version v1.32. |None |


<span id=".a3ViZXJuZXRlcy12MS0zMC3lj5jmm7TorrDlvZU="></span>
## Historical change log

<span id="62kSJIBd"></span>
### Kubernetes v1.30 change log

<span id="2ag2fM7f"></span>
#### January 2026


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.10 |Cluster version ≥ v1.30 |Being maintained |System\-managed |* Supports configuring the maximum timeout duration for node readiness waiting.<br><br>* Supports configuring scale\-down delay calculation based on the local status of node pools.<br><br>* Supports ignoring resource usage of DaemonSet pods when calculating node scale\-down thresholds. |None |


<span id="1CwDZvts"></span>
#### November 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.9 |Cluster version ≥ v1.30 |No longer maintained |System\-managed |* Optimize stability of self\-healing from abnormal node scaling.<br><br>* Optimize node scaling performance for large\-scale clusters. |None |


<span id="KCVwJPCr"></span>
#### October 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.8 |v1.30 ≤ cluster version ≤ v1.32 |No longer maintained |System\-managed |Optimize node scaling stability in CSI scenarios. |None |


<span id="_2025-06"></span>
#### June 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.5 |Cluster version = v1.30 |No longer maintained |System\-managed |Optimizes add\-on stability under large\-scale clusters. |None |


<span id="_2025-02"></span>
#### February 2025


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.3 |Cluster version = v1.30 |No longer maintained |System\-managed |* Adaptation for cloud service bootstrapping.<br><br>* Supports applying taints and ignoring taints for custom nodes. |None |


<span id="_2025-01"></span>
#### January 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.2 |Cluster version = v1.30 |No longer maintained |System\-managed |The node scale\-in concurrency has risen from 15 to 30. |None |


<span id="_2024-12"></span>
#### December 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.30.3\-vke.1 |Cluster version = v1.30 |No longer maintained |System\-managed |Adapted for Kubernetes v1.30. |None |


<span id=".a3ViZXJuZXRlcy12MS0yOC3lj5jmm7TorrDlvZU="></span>
### Kubernetes v1.28 change log

<span id="N9er3fcy"></span>
#### January 2026


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.15 |v1.28 ≤ Cluster version ≤ v1.30 |No longer maintained |System\-managed |* Supports configuring the maximum timeout duration for node readiness waiting.<br><br>* Supports configuring scale\-down delay calculation based on the local status of node pools.<br><br>* Supports ignoring resource usage of DaemonSet pods when calculating node scale\-down thresholds. |None |


<span id="Kiu3cwvu"></span>
#### November 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.14 |v1.28 ≤ Cluster version ≤ v1.30 |No longer maintained |System\-managed |Optimize stability of self\-healing from abnormal node scaling. |None |


<span id="q1aBwQEk"></span>
#### October 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.13 |v1.28 ≤ Cluster version ≤ v1.30 |No longer maintained |System\-managed |Optimize node scaling stability in CSI scenarios. |None |
|v1.28.0\-vke.12 |v1.28 ≤ Cluster version ≤ v1.30 |No longer maintained |System\-managed |Optimize functionality of self\-healing from abnormal node scaling. |None |


<span id="_2025-06"></span>
#### June 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.11 |Cluster version = v1.28 |No longer maintained |System\-managed |Optimizes add\-on stability under large\-scale clusters. |None |


<span id="_2025-02"></span>
#### February 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.9 |Cluster version = v1.28 |No longer maintained |System\-managed |* Adaptation for cloud service bootstrapping.<br><br>* Supports applying taints and ignoring taints for custom nodes. |None |


<span id="_2025-01"></span>
#### January 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.8 |Cluster version = v1.28 |No longer maintained |System\-managed |The node scale\-in concurrency has risen from 15 to 30. |None |


<span id="_2024-11"></span>
#### November 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.7 |Cluster version = v1.28 |No longer maintained |System\-managed |* Optimizes the autoscaler capability of nodes of local disk specifications.<br><br>* Before triggering the autoscaler, adds a configuration validation to the scaling group. |None |


<span id="_2024-09"></span>
#### September 2024


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.6 |Cluster version = v1.28 |No longer maintained |System\-managed |Optimizes the performance of cross\-service authorization. |None |


<span id="_2024-06"></span>
#### June 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.5 |Cluster version = v1.28 |No longer maintained |System\-managed |Optimizes the adaptation performance of system labels of autoscaler. |None |


<span id="_2024-05"></span>
#### May 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.4 |Cluster version = v1.28 |No longer maintained |System\-managed |* Supports hot updates for node pools.<br><br>* Supports configuration of parameters such as elastic sensitivity. |None |


January 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.3 |Cluster version = v1.28 |No longer maintained |System\-managed |Adjusts the relevant OpenAPI parameters. |None |
|v1.28.0\-vke.2 |Cluster version = v1.28 |No longer maintained |System\-managed |Supports triggering scaling through ResourcePolicy. |None |


<span id="_2023-11"></span>
#### November 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.28.0\-vke.1 |Cluster version = v1.28 |No longer maintained |System\-managed |Supports Kubernetes version 1.28. |None |


<span id=".a3ViZXJuZXRlcy12MS0yNi3lj5jmm7TorrDlvZU="></span>
### Kubernetes v1.26 change log

<span id="4lDEV65o"></span>
#### January 2026


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.23 |Cluster version = v1.26 |No longer maintained |System\-managed |* Supports configuring the maximum timeout duration for node readiness waiting.<br><br>* Supports configuring scale\-down delay calculation based on the local status of node pools.<br><br>* Supports ignoring resource usage of DaemonSet pods when calculating node scale\-down thresholds. |None |


<span id="yMRbx4pR"></span>
#### November 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.22 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimize stability of self\-healing from abnormal node scaling. |None |


<span id="Z2i94nx3"></span>
#### October 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.21 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimize node scaling stability in CSI scenarios. |None |


<span id="_2025-06"></span>
#### June 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.19 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimizes add\-on stability under large\-scale clusters. |None |


<span id="_2025-02"></span>
#### February 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.17 |Cluster version = v1.26 |No longer maintained |System\-managed |* Adaptation for cloud service bootstrapping.<br><br>* Supports applying taints and ignoring taints for custom nodes. |None |


<span id="_2025-01"></span>
#### January 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.16 |Cluster version = v1.26 |No longer maintained |System\-managed |The node scale\-in concurrency has risen from 15 to 30. |None |


<span id="_2024-12"></span>
#### December 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.15 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimizes the adaptation capability of GPU resources. |None |


<span id="_2024-11"></span>
#### November 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.14 |Cluster version = v1.26 |No longer maintained |System\-managed |* Optimizes the autoscaler capability of nodes of local disk specifications.<br><br>* Before triggering the autoscaler, adds a configuration validation to the scaling group. |None |


<span id="_2024-09"></span>
#### September 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.13 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimizes the performance of cross\-service authorization. |None |


<span id="_2024-06"></span>
#### June 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.12 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimizes the adaptation performance of system labels of autoscaler. |None |


<span id="_2024-05"></span>
#### May 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.11 |Cluster version = v1.26 |No longer maintained |System\-managed |* Supports hot updates for node pools.<br><br>* Supports configuration of parameters such as elastic sensitivity. |None |


<span id="_2024-01"></span>
#### January 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.10 |Cluster version = v1.26 |No longer maintained |System\-managed |Adjusts the relevant OpenAPI parameters. |None |
|v1.26.3\-vke.9 |Cluster version = v1.26 |No longer maintained |System\-managed |Supports triggering scaling through ResourcePolicy. |None |


<span id="_2023-11"></span>
#### November 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.8 |Cluster version = v1.26 |No longer maintained |System\-managed |Optimizes the scaling procedure of the node pool of the autoscaler group. |None |
|v1.26.3\-vke.7 |Cluster version = v1.26 |No longer maintained |System\-managed |* Optimizes the computing logic of the maximum pod number of nodes.<br><br>* Optimizes the timeout configuration of calling downstream services. |None |
|v1.26.3\-vke.6 |Cluster version = v1.26 |No longer maintained |System\-managed |Supports setting the scale\-in threshold of GPU nodes. For detailed description, refer to [Creating node autoscaler](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler). |None |


<span id="_2023-10"></span>
#### October 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.5 |Cluster version = v1.26 |No longer maintained |System\-managed |Fixes the computing logic of the network resources of the Trunk instances. |None |


<span id="_2023-09"></span>
#### September 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.4 |Cluster version = v1.26 |No longer maintained |System\-managed |Supports the scaling of mGPU resources. |None |


<span id="_2023-08"></span>
#### August 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.3 |Cluster version = v1.26 |No longer maintained |System\-managed |Code refactoring adapted to node pools based on the AutoScalingGroup. For information about autoscaler groups, refer to [What is autoscaler](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling). |None |


<span id="_2023-07"></span>
#### July 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.2 |Cluster version = v1.26 |No longer maintained |System\-managed |* Enhances stability and fixes restart issues caused by DNS interruptions.<br><br>* Fixes the issue of multiple scaling of node pools caused by untimely synchronization of custom labels of node pools.<br><br>* Fixes the issue of node pools being unable to scale\-in when the cooldown period is mistakenly calculated in some scenarios. |None |


<span id="_2023-06"></span>
#### June 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.26.3\-vke.1 |Cluster version = v1.26 |No longer maintained |System\-managed |Supports Kubernetes v1.26. |None |


<span id=".a3ViZXJuZXRlcy12MS0yNC3lj5jmm7TorrDlvZU="></span>
### Kubernetes v1.24 change log

<span id="_2025-06"></span>
#### June 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.17 |Cluster version = v1.24 |No longer maintained |System\-managed |Optimizes add\-on stability under large\-scale clusters. |None |


<span id="_2025-01"></span>
#### January 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.15 |Cluster version = v1.24 |No longer maintained |System\-managed |* Adaptation for cloud service bootstrapping.<br><br>* The node scale\-in concurrency has risen from 15 to 30. |None |


<span id="_2024-11"></span>
#### November 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.14 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |* Optimizes the autoscaler capability of nodes of local disk specifications.<br><br>* Before triggering the autoscaler, adds a configuration validation to the scaling group. |None |


<span id="_2024-09"></span>
#### September 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.13 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Optimizes the performance of cross\-service authorization. |None |


<span id="_2024-06"></span>
#### June 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.12 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Optimizes the adaptation performance of system labels of autoscaler. |None |


<span id="_2024-05"></span>
#### May 2024


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.11 |v1.24 ≤ Cluster version ≤ v1.26 |Being maintained |System\-managed |* Supports hot updates for node pools.<br><br>* Supports configuration of parameters such as elastic sensitivity. |None |


<span id="_2024-01"></span>
#### January 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.10 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Adjusts the relevant OpenAPI parameters. |None |
|v1.24.2\-vke.9 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Supports triggering scaling through ResourcePolicy. |None |


<span id="_2023-11"></span>
#### November 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.8 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Optimizes the scaling procedure of the node pool of the autoscaler group. |None |
|v1.24.2\-vke.7 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |* Optimizes the computing logic of the maximum pod number of nodes.<br><br>* Optimizes the timeout configuration of calling downstream services. |None |
|v1.24.2\-vke.6 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Supports setting the scale\-in threshold of GPU nodes. For detailed description, refer to [Creating node autoscaler](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler). |None |


<span id="_2023-10"></span>
#### October 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.5 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Fixes the computing logic of the network resources of the Trunk instances. |None |


<span id="_2023-09"></span>
#### September 2023


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.4 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Supports the scaling of mGPU resources. |None |


<span id="_2023-08"></span>
#### August 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.3 |v1.24 ≤ Cluster version ≤ v1.26 |Being maintained |System\-managed |Code refactoring adapted to node pools based on the AutoScalingGroup. For information about autoscaler groups, refer to [What is autoscaler](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling). |None |


<span id="_2023-07"></span>
#### July 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.24.2\-vke.2 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |* Enhances stability and fixes restart issues caused by DNS interruptions.<br><br>* Fixes the issue of multiple scaling of node pools caused by untimely synchronization of custom labels of node pools.<br><br>* Fixes the issue where the node pool\-level cooldown period was not taking effect. |None |
|v1.24.2\-vke.1 |v1.24 ≤ Cluster version ≤ v1.26 |No longer maintained |System\-managed |Kubernetes v1.24 is supported. |None |


<span id=".a3ViZXJuZXRlcy12MS0yMC3lj5jmm7TorrDlvZU="></span>
### Kubernetes v1.20 change log

<span id="_2025-06"></span>
#### June 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.31 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Optimizes add\-on stability under large\-scale clusters. |None |


<span id="_2025-01"></span>
#### January 2025


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.29 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |The node scale\-in concurrency has risen from 15 to 30. |None |


<span id="_2024-09"></span>
#### September 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.27 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Optimizes the performance of cross\-service authorization. |None |


<span id="_2024-06"></span>
#### June 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.26 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Optimizes the adaptation performance of system labels of autoscaler. |None |


<span id="_2024-05"></span>
#### May 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.25 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Supports hot updates for node pools. |None |


<span id="_2024-01"></span>
#### January 2024


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.24 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Adjusts the OpenAPI add\-on parameters |None |
|v1.20.2\-vke.23 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Supports triggering scaling through ResourcePolicy. |None |


<span id="_2023-11"></span>
#### November 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.22 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Optimizes the scaling procedure of the node pool of the autoscaler group. |None |
|v1.20.2\-vke.21 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* Optimizes the computing logic of the maximum pod number of nodes.<br><br>* Optimizes the timeout configuration when calling downstream services. |None |
|v1.20.2\-vke.20 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Supports setting the scale\-in threshold of GPU nodes. For detailed description, refer to [Creating node autoscaler](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler). |None |


<span id="_2023-10"></span>
#### October 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.19 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Fixes the computing logic of the network resources of the Trunk instances. |None |


<span id="_2023-09"></span>
#### September 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.18 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Supports the scaling of mGPU resources. |None |


<span id="_2023-08"></span>
#### August 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.17 |v1.20 ≤ Cluster version ≤ v1.24 |Being maintained |System\-managed |Code refactoring adapted to node pools based on the AutoScalingGroup. For information about autoscaler groups, refer to [What is autoscaler](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling). |None |


<span id="_2023-07"></span>
#### July 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.16 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* Enhances stability and fixes restart issues caused by DNS interruptions.<br><br>* Fixes the issue of multiple scaling of node pools caused by untimely synchronization of custom labels of node pools.<br><br>* Fixes the issue of node pools being unable to scale\-in when the cooldown period is mistakenly calculated in some scenarios. |None |


<span id="_2023-06"></span>
#### June 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.15 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Supports cooldown periods at the node pool level. |None |


<span id="_2023-05"></span>
#### May 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.14 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Optimizes the default parameter when calling API installation add\-on. |None |


<span id="_2023-04"></span>
#### April 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.13 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* Fixed issues such as inability to scale and inaccurate scaling quantities caused by changes to node pool specifications.<br><br>* Fix the issue where, during the expansion of one node pool, another node pool in the same cluster cannot scale down even after its cooldown period has expired. |None |


<span id="_2023-03"></span>
#### March 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.12 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* Improves the accuracy of scaling.<br><br>* Fixes the issue of Panic anomaly that the add\-on occasionally encounters. |None |


<span id="_2023-02"></span>
#### February 2023


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.11 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Supports both managed and unmanaged deployment models.<br><br><br>* Managed deployment model: You do not need to upgrade and maintain the add\-on which will be managed by the system.<br><br>* Unmanaged deployment model: Supports self\-upgrading the add\-on. For detailed operations, refer to [Upgrading add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on). |None |


<span id="_2023-01"></span>
#### January 2023


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.10 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* Fixes the issue of the cluster\-autoscaler add\-on having no responses caused by massive Pending Pods.<br><br>* Fixes the issue where new nodes are deleted due to too short a scale\-in cooldown time in VPC\-CNI network model clusters.<br><br>* Fixes the issue of multiple scaling of nodes caused by estimation errors under the clusters of VPC\-CNI network models. |None |


<span id="_2022-12"></span>
#### December 2022


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.9 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* Adapted to cello v1.4.0.<br><br>* Fixes calculation errors for the expected number of node pool copies in start and stop modes. |None |
|v1.20.2\-vke.8 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* The number of nodes which are scaling simultaneously is limited to 90 in a single node pool.<br><br>* Enhances add\-on stability during network jitters. |None |
|v1.20.2\-vke.7 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Enhances the reliability of add\-on deployment. |None |


<span id="_2022-11"></span>
#### November 2022


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.6 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |Enhances add\-on stability during network jitters. |None |
|v1.20.2\-vke.5 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |* The number of nodes which are scaling simultaneously is limited to 90 in a single node pool.<br><br>* Fixes the issue where node pool scaling cannot be triggered when a Pod uses some node labels for scheduling. |None |


<span id="_2022-10"></span>
#### October 2022


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.4 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |System\-managed |The deployment model changes from unmanaged to managed, which means you do not need to upgrade and maintain the add\-on of this version and versions later installed. The add\-on is managed by the system. |This is the first system\-managed version which cannot be upgraded from the earliest version to this version. You can only uninstall and reinstall. |


<span id="_2022-09"></span>
#### September 2022


|Version |Compatibility with Kubernetes version |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.3 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |Unmanaged |Fixes the issue of authentication failures that occasionally occur. |None |


<span id="_2022-08"></span>
#### August 2022


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.2 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |Unmanaged |* The node pool that supports starting and stopping modes.<br><br>* Fixes the issue of estimation errors leading to inaccurate number of newly scaled nodes under the cluster of the VPC\-CNI network model. |None |


<span id="_2022-07"></span>
#### July 2022


|Version |Kubernetes version compatibility |Version status |Deployment mode |Description |Upgrade impact |
|---|---|---|---|---|---|
|v1.20.2\-vke.1 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |Unmanaged |Refactoring of this version to improve the stability of the cluster\-autoscaler add\-on. |None |
