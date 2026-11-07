---
title: "ingress-nginx"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ingress-nginx"
---

The ingress\-nginx add\-on provided by Vital Kubernetes Engine (VKE) is an Ingress controller that uses Nginx as both the reverse proxy and load balancer. This topic describes the change history of the ingress\-nginx add\-on.

For more information and usage instructions on add\-ons, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="ZEUQCMQs"></span>
## March 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.14.3\-vke.1 |Cluster version: v1.26 to v1.34 |Being maintained<br><br><div data-tips="true" data-tips-type="tip">Description</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>] This version is in the <strong>beta</strong> stage. To use it, submit an application.</div><br> |Fixed ingress\-nginx security vulnerability [CVE-2026-1580](https://github.com/kubernetes/kubernetes/issues/136677) to align with the community version 1.14.3. |* This version implements stricter validation on Ingresses that contain regular expressions. When regular expressions are used in Ingress configuration, `pathType` must be set to `ImplementationSpecific`.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your cluster contains regular expression\-based Ingresses and <code>pathType</code> is not <code>ImplementationSpecific</code>, first set <code>pathType</code> to <code>ImplementationSpecific</code> before upgrading the add\-on.   </div><br>   <br><br>* We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2025-04"></span>
## April 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.11.5\-vke.2 |Cluster version: v1.26 to v1.34 |Being maintained |* Fixes the issue where the add\-on cannot be installed as a VCI pod in v1.11.5\-vke.1.<br><br>* Synchronizes with community v1.11.5 to patch ingress\-nginx security vulnerabilities.<br><br>   * [CVE-2025-1097](https://github.com/kubernetes/kubernetes/issues/131007)<br><br>   * [CVE-2025-1098](https://github.com/kubernetes/kubernetes/issues/131008)<br><br>   * [CVE-2025-1974](https://github.com/kubernetes/kubernetes/issues/131009)<br><br>   * [CVE-2025-24513](https://github.com/kubernetes/kubernetes/issues/131005)<br><br>   * [CVE-2025-24514](https://github.com/kubernetes/kubernetes/issues/131006) |Note the following information when you upgrade ingress\-nginx to this version:<br><br><br>* The v1.11.5 community version sets `AllowSnippetAnnotations` to off by default. This switch indicates whether you can use `*-snippet annotations` on Ingresses. If your cluster uses `*-snippet` annotations, add `allow-snippet-annotations: true` to the ingress\-nginx ConfigMap before upgrading the add\-on version.<br><br>* We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |
|v1.11.5\-vke.1 |Cluster version: v1.26 to v1.32 |Being maintained |Synchronizes with the open\-source community v1.11.5 release to address the following security vulnerabilities in ingress\-nginx:<br><br><br>* [CVE-2025-1097](https://github.com/kubernetes/kubernetes/issues/131007)<br><br>* [CVE-2025-1098](https://github.com/kubernetes/kubernetes/issues/131008)<br><br>* [CVE-2025-1974](https://github.com/kubernetes/kubernetes/issues/131009)<br><br>* [CVE-2025-24513](https://github.com/kubernetes/kubernetes/issues/131005)<br><br>* [CVE-2025-24514](https://github.com/kubernetes/kubernetes/issues/131006) |Note the following information when you upgrade ingress\-nginx to this version:<br><br><br>* The v1.11.5 community version sets `AllowSnippetAnnotations` to off by default. This switch specifies whether you can use `*-snippet annotations` on Ingresses. If your cluster uses `*-snippet` annotations, add `allow-snippet-annotations: true` to the ingress\-nginx ConfigMap before upgrading the add\-on version.<br><br>* We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2024-10"></span>
## October 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.10.4\-vke.1 |Cluster version ≥ v1.26 |Being maintained |* Synchronizes with the open\-source community v1.11.5 release and fixes the ingress\-nginx security vulnerability CVE\-2024\-7646. For detailed information about the vulnerability, refer to [issue](https://github.com/kubernetes/kubernetes/issues/126744).<br><br>* This version is currently in canary release. To use it, contact your account manager to submit an application. |You need to note the following items when upgrading the ingress\-nginx add\-on from earlier versions to this version:<br><br><br>* The v1.10.4 community version sets AllowSnippetAnnotations to off by default. This switch specifies whether you can use `*-snippet` annotations on Ingresses. If your cluster uses `*-snippet` annotations, add `allow-snippet-annotations: true` to the ingress\-nginx ConfigMap before upgrading the add\-on version.<br><br>* We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2024-04"></span>
## April 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.9.5\-vke.2 |Cluster version: v1.28 and later |Being maintained |* The installation of this add\-on supports configuring the CLB instance specification, availability zone, modification protection, and billing types.<br><br>* Updating this add\-on supports updating CLB instance specification, modification protection, and billing types. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |
|v1.9.5\-vke.1 |Cluster version: v1.28 and later |Being maintained |Supports Kubernetes version 1.28. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2023-12"></span>
## December 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.6.4\-vke.3 |Cluster version: v1.24 to v1.26 |Being maintained |Supports configuring an EIP shared bandwidth package on the CLB instance associated with the Service corresponding to ingress\-nginx\-controller. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |
|v1.3.1\-vke.6 |Cluster version: v1.20 to v1.24 |Being maintained |Supports configuring an EIP shared bandwidth package on the CLB instance associated with the Service corresponding to ingress\-nginx\-controller. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2023-04"></span>
## April 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.1\-vke.5 |Cluster version: v1.20 to v1.24 |Being maintained |Opens up the Prometheus monitoring metrics by default, and allows monitoring the ingress\-nginx add\-on through the Vital Managed Service for Prometheus (VMP). For more information, refer to [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability). |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2023-02"></span>
## February 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.1\-vke.4 |Cluster version: v1.20 to v1.24 |Being maintained |Resolves the log collection issue in elastic container deployment mode. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2023-01"></span>
## January 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.1\-vke.3 |Cluster version: v1.20 to v1.24 |Being maintained |Optimizes the add\-on deployment architecture. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2022-12"></span>
## December 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.1\-vke.2 |Cluster version: v1.20 to v1.24 |No longer maintained |Supports high\-availability deployment of the add\-on. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2022-10"></span>
## October 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.3.1\-vke.1 |Cluster version: v1.20 to v1.24 |No longer maintained |* Supports Kubernetes version v1.24.<br><br>* Enhances add\-on security. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2022-06"></span>
## June 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.1\-vke.2 |Cluster version = v1.20 |Being maintained |* Adds the deep detection feature for Ingress objects and enables it by default. Stops writing to Ingress configurations that contain sensitive fields.<br><br>   This feature fixes the [CVE-2021-25745](https://nvd.nist.gov/vuln/detail/CVE-2021-25745) issue.<br><br>* Supports configuring annotation\-value\-word\-blocklist to block writing of Ingress annotations that contain sensitive fields.<br><br>   This feature fixes the [CVE-2021-25746](https://nvd.nist.gov/vuln/detail/CVE-2021-25746) issue.<br><br>* Adds the default IngressClass object. The Ingress that has not been configured with the IngressClass will be handled by the default Ingress Nginx controller.<br><br>* Resolves several stability issues. |* Before upgrading, check whether there are sensitive fields in the existing Ingress configurations.<br><br>   After the upgrade, Ingresses containing sensitive fields will no longer take effect (sensitive fields include but are not limited to `load_module`, `lua_package`, `_by_lua`, `location`, `root`, `proxy_pass`, `serviceaccount`, `{`, `}`, `'`, and `"`).<br><br>* We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2022-02"></span>
## February 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.49.3\-vke.1 |Cluster version < v1.20 |No longer maintained |Optimizes the default Nginx configuration. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2022-01"></span>
## January 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.49.3 |Cluster version < v1.20 |No longer maintained |* Add the `allow-snippet-annotations` annotation to mitigate the [CVE-2021-25742](https://nvd.nist.gov/vuln/detail/CVE-2021-25742) vulnerability.<br><br>* Resolves several stability issues. |We recommend you upgrade the add\-on during the off\-peak business period. During the changes, the already established connections might encounter transient interruptions, but will automatically resume after the changes. |


<span id="_2021-10"></span>
## October 2021


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.44.0 |Cluster version < v1.20 |No longer maintained |The ingress\-nginx add\-on was released for the first time. |None |
