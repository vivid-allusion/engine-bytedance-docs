---
title: "vpc-cni-controlplane"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/vpc-cni-controlplane"
---

The vpc\-cni\-controlplane add\-on is the VPC\-CNI control plane add\-on of clusters, which provides control plane management capability for configuring security groups for Pods. This topic describes the change history of the vpc\-cni\-controlplane add\-on.

For more information about the add\-on and how to use it, see [vpc-cni-controlplane](https://docs.byteplus.com/en/docs/vke/vpc-cni-controlplane-add-on?lang=en).

<span id="4xBw0V4e"></span>
## August 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.6.7 |v1.20 ≤ Cluster version ≤ v1.36 |Being maintained |Availability zone matching accuracy during fixed IP reuse is improved to prevent inconsistencies between scheduling results and the actual bound network interface. |None |
|v1.6.6 |v1.20 ≤ Cluster version ≤ v1.36 |No longer maintained |* Fixed IP Pods can now be recreated with the same name by reusing the existing network interface and the original fixed IP address when VED is temporarily unavailable. This reduces the risk of business recovery being blocked during maintenance or abnormal states.<br><br>* We fixed an issue with abnormal network interface cleanup after fixed IP Pods on VCI are deleted. This prevents unintended cloud\-side ENI cleanup when labels are cleared after unbinding, which could otherwise block resource deletion for an extended period. |None |


<span id="OKIHKNVj"></span>
## July 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.6.4 |v1.20 ≤ Cluster version ≤ v1.36 |Being maintained |* Trunk/VED: `unavailableSubnets` can be displayed in `VPCENIDefinition.status`, and availability zones of unavailable subnets can be included in considerations for Pod affinity scheduling via annotations.<br><br>* VPCENIDefinition: The reconciliation interval is adjusted for scenarios where subnets are unavailable or all subnets are in the NoAvailableIP state, and ReadyWithNoAvailableIP is used to indicate a special Ready state. | |
|v1.6.3 |All versions |Being maintained |Fixes the validation of EIP tags. |None |
|v1.6.2 |All versions |No longer maintained |* Adds support for specifying tags during EIP creation.<br><br>* Optimizes the subnet selection algorithm for vpceni. |None |


<span id="mMDpqROZ"></span>
## June 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.6.1 |All versions |Being maintained |Optimizes the retry frequency for add\-on errors. |None |


<span id="2GN3HwOw"></span>
## January 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.5.3 |All versions |Being maintained |Supports binding public IPv6 network bandwidth to Pods. |None |


<span id="wGnW3Gmu"></span>
## April 2025


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.4.5 |All versions |Being maintained |* Supports vRDMA.<br><br>* Fixes the VPCENI TTL calculation.<br><br>* Fixes the VPCENI recycling logic when a cluster is deleted.<br><br>* Supports fixed IP addresses for VCI. |None |


<span id="HWFm2r1b"></span>
##
