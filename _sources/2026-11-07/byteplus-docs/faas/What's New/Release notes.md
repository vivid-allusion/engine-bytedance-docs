---
title: "Release notes"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Release_notes"
---

This topic describes the release notes for BytePlus Function Service (veFaaS). New features will be rolled out across regions. We are looking forward to your hands\-on experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>Region</strong> column displays the regions where the features were first released. For the regions where features are available, the regions displayed in the console shall prevail.</div>


<span id="QmlDIJVw"></span>
## August 2026


|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|Cloud sandbox applications support custom DNS |You can configure custom DNS servers and host resolution rules for sandbox applications to meet requirements such as custom DNS resolution within sandbox instances and access to internal network services. |All |[Advanced configurations for sandbox applications](https://docs.byteplus.com/en/docs/faas/Advanced_configuration_for_sandbox_applications) |


<span id="GovR0kl9"></span>
## March 2026


|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|Cloud sandboxes supporting route authentication configuration |Cloud sandboxes support configuring route authentication. Users can use the Key Auth plugin through APIG to implement API Key\-based authentication and authorization. This ensures the route security of sandbox applications. |All |[Sandbox application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications) |
|Cloud sandboxes supporting warm pools |Through a unified product solution, veFaaS offers sandbox instance warm pool capabilities, enabling centralized governance and observability of the warm pool and significantly reducing instance startup duration. |All |[Sandbox instance warm pools](https://docs.byteplus.com/en/docs/faas/Sandbox_instance_warm_pools) |


<span id="oCP5yC5y"></span>
## December 2025

<span id="uOi0JcsK"></span>
## 
|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|Sandbox image filtering by type |Public sandbox images can be filtered by type, which improves filtering efficiency. |All |[For sandbox images](https://docs.byteplus.com/en/docs/faas/Sandbox_images) |
|Custom runtime |A runtime that meets business requirements can be created through custom images. |All |[Creating custom runtimes](https://docs.byteplus.com/en/docs/faas/Create_a_custom_runtime) |


<span id="JlXwL42D"></span>
## November 2025


|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|CLB support for microservices apps |Microservices apps allow you to specify a CLB instance as the traffic entry point. |All |[Adding CLB access configurations](https://docs.byteplus.com/en/docs/faas/Adding_CLB_access_configurations) |
|Wildcard domains supported for sandbox applications |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features)] In the sandbox environment, a service contains multiple sandboxes and shares a public access address. Through a wildcard domain, each sandbox can be assigned a unique subdomain to implement independent access. |All |[Wildcard domain configuration for sandbox applications](https://docs.byteplus.com/en/docs/faas/Configuring_wildcard_domains_for_sandbox_applications) |


<span id="tKbvrwxO"></span>
## September 2025


|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|Management optimizations for sandbox applications |Sandbox applications support manual release, rollback, and version management. |All |[Sandbox application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications) |
|Health check |Microservices functions support health checking. |All |[Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration) |
|Debugging |In native runtime scenarios for web apps, container debugging supports the WebIDE debugging method. |All |[Debugging](https://docs.byteplus.com/en/docs/faas/Debugging) |


<span id="YDn6TAp2"></span>
## July 2025


|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|Price reductions are applied to some billing items. |Price reductions are applied to some billing items in the Asia Pacific (Johor) region, such as the unit of the number of function invocations, the number of function invocations, and CPU instance resource usage. |Asia Pacific (Johor) |[[Billing updates] Notification on the changes in veFaaS partial unit prices](https://docs.byteplus.com/en/docs/faas/Billing-updates-FaaS-pricing-updates) |
|The configuration of the asynchronous task feature is optimized. |When the asynchronous task feature is in non\-webserver mode, the exclusive mode is used by default, and a single instance cannot process multiple concurrent requests. This improves the success rate of asynchronous task creation. |All |* [Configuring asynchronous tasks](https://docs.byteplus.com/en/docs/faas/Configuring_async_tasks)<br><br>* [Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration) |
|veFaaS is commercially available. |veFaaS has ended its public beta on BytePlus and is now officially commercially available. |All |[Product features](https://docs.byteplus.com/en/docs/faas/Features) |


<span id=".MjAyNeW5tDAy5pyI"></span>
## March 2025


|**Feature** |**Description** |**Region** |**Related document** |
|---|---|---|---|
|veFaaS |The first public beta of BytePlus Function Service(veFaaS) is released on BytePlus. |All |[Product features](https://docs.byteplus.com/en/docs/faas/Features) |
