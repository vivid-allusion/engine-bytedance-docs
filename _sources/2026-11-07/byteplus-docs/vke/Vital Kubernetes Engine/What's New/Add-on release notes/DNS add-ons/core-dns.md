---
title: "core-dns"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/core-dns"
---

The core\-dns add\-on provides service discovery and Domain Name System (DNS) resolution services in clusters. This topic describes the change history of the core\-dns add\-on.

For more information about add\-ons, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id=".6YWN572u6K-05piO"></span>
## Description


* When you upgrade the add\-on, the configurations displayed in the console will be retained for each version.

* The retention of user\-defined configurations is not guaranteed for each version. For details, see the descriptions in the **Impact** column.


<span id=".54mI5pys5Y-Y5pu0"></span>
## Version changes

<span id="rghbIUJr"></span>
### November 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.12.4 |Cluster version: v1.32 to v1.36 |Maintained |* Supports Kubernetes v1.36.<br><br>* Upgrades the CoreDNS add\-on (community version) to v1.12.4. |For impacts, see [Coredns-v1.12.4-Release](https://github.com/coredns/coredns/releases/tag/v1.12.4). |


<span id="VCLtYZz9"></span>
### June 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.11.3 |v1.30 ≤ cluster version ≤ v1.32 |Maintained |Kubernetes v1.32 is supported. |None |


<span id="4CPI77Jn"></span>
### December 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.11.1 |Cluster version: v1.28 to v1.30 |Maintained |Kubernetes v1.30 is supported. |None |
|v1.10.1\-vke.201 |Cluster version: v1.24 to v1.26 |Maintained |The requests and upper limits of CPU and memory resources, node affinity, and pod scheduling based on taints and tolerations of the add\-on replicas can be configured. For details, see [core-dns](https://docs.byteplus.com/en/docs/vke/core-dns-add-on). |None |
|v1.10.1\-vke.401 |Cluster version: v1.26 to v1.28 |Maintained |||


<span id="_2024-08"></span>
### August 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.10.1\-vke.200 |Cluster version: v1.24 to v1.26 |Maintained |* The CPU or memory requests of the replicas (pods) for the core\-dns add\-on can be configured. For details, see [core-dns](https://docs.byteplus.com/en/docs/vke/core-dns-add-on).<br><br>* The default CPU or memory request for a single replica of the add\-on is changed from `100 millicores/70 MiB` to `2 cores/4 GiB`.<br><br>* The concurrency limit of the external domain name request forwarding feature is adjusted to 10,000 QPS to meet the high concurrency requirements of online businesses.<br><br>* The maximum number of intolerable pods (maxUnavailable) during the add\-on rolling update process is adjusted to 0 to ensure that the configuration requirements are met in extreme cases. |* Because the default CPU and memory requests for add\-on replicas have increased, the corresponding pods may remain in the Pending state during installation if node resources are insufficient. Make sure that the cluster has sufficient ECS nodes to schedule the component Pods, or deploy the components using VCI.<br><br>* The higher the DNS request QPS and the higher the proportion of external domain names, the greater the CPU consumption of the core\-dns add\-on.<br><br>* The increase in the number of business pods and services in clusters will lead to higher memory usage of the core\-dns add\-on.<br><br>* The performance limits of the add\-on are changed. For details, see [Limit](https://docs.byteplus.com/en/docs/vke/Limits). |
|v1.10.1\-vke.400 |Cluster version: v1.26 to v1.28 |Maintained |||


<span id="_2024-03"></span>
### January 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.10.1\-vke.1 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |The add\-on is compatible with DCP. |None |


<span id="_2023-11"></span>
### November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.10.1 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |The add\-on is upgraded in alignment with the community CoreDNS. |For impacts, see [Coredns-v1.10.1-Release](https://github.com/coredns/coredns/releases/tag/v1.10.1). |


<span id="_2023-07"></span>
### July 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.9.3\-vke.1 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |The add\-on is upgraded in alignment with the community CoreDNS. |None |


<span id="_2023-06"></span>
### June 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.9.3 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |The add\-on is upgraded in alignment with the community CoreDNS. |For impacts, refer to the following official documentation of CoreDNS:<br><br><br>* [CoreDNS-1.8.7-release](https://coredns.io/2021/12/09/coredns-1.8.7-release/)<br><br>* [CoreDNS-1.9.0 Release](https://coredns.io/2022/02/01/coredns-1.9.0-release/)<br><br>* [CoreDNS-1.9.1 Release](https://coredns.io/2022/03/09/coredns-1.9.1-release/)<br><br>* [CoreDNS-1.9.2 Release](https://coredns.io/2022/05/13/coredns-1.9.2-release/)<br><br>* [CoreDNS-1.9.3 Release](https://coredns.io/2022/05/27/coredns-1.9.3-release/) |


<span id="_2023-05"></span>
### May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.6\-vke.4 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |User\-defined configurations can be retained after the add\-on is upgraded. |* During the upgrade process, the system will keep the CoreDNS configuration (the content of the Corefile in the CoreDNS ConfigMap in the kube\-system namespace) for you by default. In addition, the content modified by yourself, such as the Limits and Requests of Deployment, may be overwritten by the system.<br><br>* If the pre\-upgrade version is lower than 1.8.6 (excluding 1.8.6 itself) and the Corefile has been manually modified to use external plugins (such as dnstap), include "transfer" statements, or contain sections referencing Caddy, incompatibilities may occur during the upgrade process. In such cases, you need to manually modify the Corefile to resolve these issues. For details, see the [official documentation of CoreDNS](https://github.com/coredns/coredns/blob/master/notes/coredns-1.8.0.md).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To enhance the stability of the DNS resolution service in clusters, we recommend that you upgrade the core\-dns add\-on to the latest version. Before you upgrade the core\-dns add\-on, carefully read the <a href="https://github.com/coredns/coredns/tree/master/notes">official release notes of CoreDNS</a>.</div><br> |


<span id="_2023-04"></span>
### April 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.6\-vke.3 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |IPv4/IPv6 dual\-stack is supported. |None |


<span id="_2023-02"></span>
### February 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.6\-vke.2 |N/A |No longer maintained |The core\-dns add\-on first schedules nodes that cannot be scaled. |None |


<span id="_2022-11"></span>
### November 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.8.6\-vke.1 |N/A |No longer maintained |Supports topology spread configuration. |None |
|v1.8.6 |N/A |No longer maintained |Kubernetes v1.24 is supported. |None |
|v1.7.0\-vke.2 |N/A |No longer maintained |Supports topology spread configuration. |None |


<span id="_2022-10"></span>
### October 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.7.0\-vke.1 |N/A |No longer maintained |The core\-dns add\-on is officially released for the first time. |None |
