---
title: "vpc-cni"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/vpc-cni"
---

The vpc\-cni add\-on is a network add\-on for clusters and supports the VPC\-CNI network model. This topic describes the change history of the vpc\-cni add\-on.

<span id="SaY681vn"></span>
## Usage instructions

For the vpc\-cni upgrade steps and validation method, see [vpc-cni](https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on). For more information about add\-ons and how to use them, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<span id="03I9T2K0"></span>
## Change log

<span id="2ieMXMOB"></span>
### July 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.12 |v1.24 ≤ Cluster version ≤ v1.36 |Being maintained |None |None |


<span id="arP5LubJ"></span>
### May 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.9.8 |v1.24 ≤ Cluster version ≤ v1.36 |Being maintained |Fixed the issue of service backend leak in the Cilium data plane. |None |


<span id="6dNgRbQE"></span>
### November 2025


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.11 |All versions |Being maintained |* Feature updates<br><br>   * The NetworkPolicy performance is optimized.<br><br>   * Service Loadbalancer IPMode is supported.<br><br>   * A larger number of services and endpoints are supported.<br><br>   * Cello\-operator can be independently deployed to optimize the performance of large\-scale clusters.<br><br>   * Pods can use IPv6\-only addresses.<br><br>   * Queue depth can be configured for auxiliary NICs used by pods.<br><br>   * The RDMA shared\-host mode is supported.<br><br>* Bug fixing<br><br>   * The issue where the ENI device plugin fails to report eni\-ip in some scenarios is fixed.<br><br>   * Connectivity issues in some scenarios after NetworkPolicy is enabled are fixed.<br><br>   * Multiple issues in scenarios where only IPv6 is used are fixed.<br><br>   * The issue where the IP addresses of pods are unexpectedly released in some scenarios is fixed.<br><br>   * Multiple issues with RDMA IPAM are fixed.<br><br>* Others<br><br>   * Version compatibility verification in upgrade scenarios is enhanced.<br><br>   * RBAC is optimized, which narrows the scope of permissions.<br><br>   * Multiple metrics are added. |None |


<span id="_2025-01"></span>
### January 2025


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.7.10 |All versions |Being maintained |* Supports specifying a Service Endpoint for OpenAPI.<br><br>* Supports dual RDMA network planes for computing and storage.<br><br>* Optimizes the pooling logic of IP Address Management (IPAM), so that metadata validation is no longer needed when requesting and releasing IP addresses.<br><br>* Adds validation logic for the RDMA routes returned by metadata. |None |


<span id="_2024-08"></span>
### October 2024


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.2 |All versions |No longer maintained |* Feature updates<br><br>   * Supported the ipMode feature. After this feature is enabled, traffic routed from Pods to Services of the LoadBalancer type will be directly routed to the load balancer.<br><br>   * When RDMA ACL is enabled, informer optimization is enabled by default.<br><br>   * Improved the efficiency of releasing IPs to the resource pool.<br><br>   * Supported configuring filtering policies for Kubernetes events.<br><br>   * Supported the cold migration of RDMA machines.<br><br>* Bug fixing<br><br>   * Fixed the issue where, on large\-scale machines, cilium kept crashing during the initialization phase of a restart due to a garbage collection timeout in the connection tracking (CT) map.<br><br>   * Fixed the issue where cilium kept crashing during startup after all available service IDs were used up.<br><br>* Others<br><br>   * Reduced the RBAC permissions of cello\-service\-account to the minimum permissions to eliminate security vulnerabilities. |None |


<span id="97wzc54p"></span>
### August 2024


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.7.9 |All versions |Being maintained |* Obtaining HPC routes through metadata API is supported.<br><br>* Omits the handling of pod\-networks in the Cello\-agent, and fixes the false positive ParsePodFailed events.<br><br>* The option `disable-cnp-status-updates` of cilium is set to `true` by default.<br><br>* Adds RDMA CNI.<br><br>* Supports the AArch64 (ARM64) architecture.<br><br>* Uses Protobuf as the default serialization format for communicating with API Server.<br><br>* Optimizes IPAM logic and fixes several known issues.<br><br>* Supports removing the Pod subnet.<br><br>* Istio compatibility mode is supported.<br><br>* Adjusts container resource usage.<br><br>* Optimizes data plane performance in Trunk mode.<br><br>* Fixes issues related to NetworkPolicy. |None |


<span id="_2024-03"></span>
### March 2024


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.6.8 |All versions |Being maintained |* Supports IPv6.<br><br>* Supports the use of Trunk ENI by Pods.<br><br>* Supports configuration of subnets and security groups at the node level.<br><br>* Supports the NetworkPolicy capability.<br><br>* Optimizes IPAM logic and fixes related issues.<br><br>* Optimizes system and kernel compatibility, and fixes relevant issues. |None |


<span id="_2023-10"></span>
### October 2023


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.5.2 |Cluster version: earlier than v1.26 |Being maintained |Fixes the issue of service traffic interruption during the upgrade of the CentOS\-compatible version. |None |


<span id="_2023-05"></span>
### May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.5.1 |Cluster version: earlier than v1.26 |Being maintained |Fixes an issue in Version v1.5.0 where some pod IPs are mistakenly released when the informer is having anomalies. |None |


<span id="_2023-03"></span>
### March 2023


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v1.5.0 |Cluster version: earlier than v1.26 |Being maintained |Optimizing and refactoring code related to the add\-on. |None |


<span id="_2022-11"></span>
### November 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.4.0 |Cluster version: earlier than v1.26 |No longer maintained |* Optimizes image size.<br><br>* Supports the Kubernetes device plugin to report elastic network interface (ENI) resources.<br><br>* Supports the dynamic scaling of subnets. |None |
