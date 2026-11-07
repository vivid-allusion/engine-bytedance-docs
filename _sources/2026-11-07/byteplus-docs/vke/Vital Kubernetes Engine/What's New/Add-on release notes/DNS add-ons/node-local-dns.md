---
title: "node-local-dns"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/node-local-dns"
---

The node\-local\-dns add\-on provides local Domain Name System (DNS) cache proxy to enhance the DNS service discovery performance and stability of the cluster. This topic includes the change logs of the node\-local\-dns add\-on.

For more information and usage instructions on add\-ons, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="c6MKWUl5"></span>
## January 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.4 |v1.24 ≤ cluster version ≤ v1.36 |Being maintained |Added support for configuring add\-on resources by using the console. |No |


<span id="_2025-04"></span>
## April 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.3 |cluster version ≤ v1.32 |Being maintained |* The add\-on security issues are addressed.<br><br>* A feature configuration switch is injected into the add\-on by default.<br><br>* The DNS cache feature is injected into VCI pods by default.<br><br>* The issue where newly added fields in Kubernetes v1.27 and later are mistakenly deleted during the injection of Pod DNS Config is fixed. |After you upgrade the add\-on, if you do not want to inject the DNS cache feature into VCI pods by default, you can use the label: `dns-config-injection: disable` on the pods or namespaces to disable the injection. |


<span id="_2024-04"></span>
## April 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.3.0 |Cluster version: earlier than v1.30 |Being maintained |The add\-on stability is improved. |No |


<span id="_2024-01"></span>
## January 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.3 |Cluster version: earlier than v1.26 |Being maintained |The add\-on is adapted to edge scenarios. |No |


<span id="_2023-11"></span>
## November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.2 |Cluster version: earlier than v1.26 |Being maintained |Custom dnsConfig configurations can be merged. |No |


<span id="_2023-09"></span>
## September 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.1 |Cluster version: earlier than v1.26 |Being maintained |The node\-local\-dns\-admission add\-on can be deployed across multiple availability zones. |No |


<span id="_2023-05"></span>
## May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.0 |Cluster version: earlier than v1.26 |Being maintained |The cluster local domain names are supported. For the descriptions of related features, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). |No |


<span id="_2023-04"></span>
## April 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.0 |All versions |No longer maintained |The node\-local\-dns add\-on is released for the first time. |No |
