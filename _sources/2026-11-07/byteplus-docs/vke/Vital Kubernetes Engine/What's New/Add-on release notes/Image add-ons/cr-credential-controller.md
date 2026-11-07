---
title: "cr-credential-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/cr-credential-controller"
---

The cr\-credential\-controller add\-on enables you to pull private images from Container Registry (CR) without a password when creating applications in VKE clusters. This topic mainly describes the change history of the cr\-credential\-controller add\-on. For more information about the add\-on and how to use it, refer to [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id=".6YWN572u6K-05piO"></span>
## Configuration description


* When you upgrade the add\-on, the configurations displayed in the console will be retained for each version.

* The retention of user\-defined configurations is not guaranteed for each version. The descriptions displayed in the **Impact** column shall prevail.


<span id=".54mI5pys5Y-Y5pu0"></span>
## Version changes

<span id="_2025-02"></span>
### February 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.3 |All versions |Maintained |* The add\-on is adapted to Region Endpoint.<br><br>* The add\-on is adapted to the decoupling of the metadata server. |None |


<span id="_2024-04"></span>
### April 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.2 |All versions |Maintained |The add\-on is adapted to the multi\-domain capability of CR. You can configure multiple access domain names for a single CR instance in the add\-on. |None |


<span id="_2023-12"></span>
### December 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.1 |All versions |Maintained |Labels related to Distributed Cloud Native Platform (DCP) are supported. |None |


<span id="_2023-10"></span>
### October 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.0 |All versions |Maintained |The add\-on parameter naming is standardized. For more details, refer to [CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon#cr-credential-controller). |None |


<span id="_2023-07"></span>
### July 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.1 |All versions |Maintained |The ConfigMap of the cr\-credential\-controller add\-on supports Webhook configuration. |None |


<span id="_2023-06"></span>
### June 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.9 |All versions |Maintained |The versions of code repositories that the add\-on depends on, such as the Golang version, are upgraded. |None |


<span id="_2023-05"></span>
### May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.8 |All versions |Maintained |The issue where the password\-free mechanism becomes invalid due to ServiceAccount being overridden is fixed. |None |


<span id="_2023-04"></span>
### April 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.7 |All versions |Maintained |* The residual resource issue is fixed..<br><br>* The delayed configuration effect issue is fixed. |None |


<span id="_2023-03"></span>
### March 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.6 |All versions |No longer maintained |The memory usage is optimized. |When you create a Helm application, if ServiceAccount is overridden, the ServiceAccount\-based password\-free mechanism may not take effect. If you encounter issues during the upgrade, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for technical support. |


<span id="_2023-02"></span>
### February 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.5 |All versions |No longer maintained |The issue of resources being overwritten is fixed. |None |


<span id="_2023-01"></span>
### January 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.4 |All versions |No longer maintained |The Vital Container Instance (VCI) deployment mode is supported. |None |
