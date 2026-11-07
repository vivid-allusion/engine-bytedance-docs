---
title: "Version Management"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Version_Management"
---

API gateway instances include multiple versions, and the scope of features supported by each version varies. This article provides a detailed introduction to the relevant information and features of each version of the API gateway instance.

<span id="MtOzhUqb"></span>
## Version description

API gateway instances use version numbers in the `x.y.z` format, for example, `3.3.0`.   


* `x`This refers to the major version number, which is upgraded only in scenarios involving changes to the gateway architecture, Istio version upgrades, and similar cases.

* `y`The middle version number is primarily related to feature updates, and some features are only supported in specified version numbers. For details, refer to the following text.

* `z`Minor version numbers are mainly used for scenarios such as defect fixes.


<span id="vyrK0mnP"></span>
## Version updates

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Versions earlier than 4.0.0: When services access the public network, traffic will be forwarded through the NAT gateway within APIG's own VPC.</div>


* <div data-tips="true" data-tips-type="default">Version 4.0.0 and above: After you enable a public NAT gateway in your own VPC, APIG can properly access backend services of the public network type. For details about enabling public NAT, refer to  <a href="https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway">Create a public NAT gateway</a>.</div>



The versions and descriptions currently supported by API gateway instances are shown in the table below.


|Gateway version |Release Date |Version description |Description |
|---|---|---|---|
|4.0.0 |2025\-10\-16 |* Supports OAuth2 Single Sign\-On (SSO) Plugin.<br><br>* Upstream public network traffic will be forwarded out through the NAT gateway within your VPC. |No |
|3.4.0 |2025\-08\-21 |Add an AI Fallback feature. |No |
|3.3.0 |2025\-05\-22 |* Upstream has added an AI model proxy.<br><br>* Added an LLM load\-aware routing plugin that supportsproviding load balancing capabilities better suited for inference scenarios based on backend GPU load conditions (for example, the number of queued requests, KV\-Cache utilization, and more).<br><br>* Added LLM Session affinity routing plugin, supports scenarios based on model inference, providing the capability to forward requests with the same session ID in multi\-turn conversations to the same instance, while distributing requests with different session IDs as much as possible. |No |
|3.2.0 |2025\-04\-15 |A new MCP session persistence plugin has been added, supporting multi\-instance session persistence based on the MCP protocol. |No |
|3.1.1 |2025\-04\-05 |Add a global rate limiting plugin, which can only be configured through OpenAPI. |No |
|3.1.0 |2025\-03\-21 |A new Key Auth plugin has been added, supporting API\-Key authentication. |No |
|3.0.0 |2024\-07\-08 |Fully supports connecting to Vital Kubernetes Engine Flannel network clusters. |No |
|2.0.0 |2024\-06\-14 |* Added support for importing the MSE registration center, enabling services registered in MES Nacos to be abstracted as an Upstream and used as the backend for the gateway.<br><br>* Upstream supports configuration of preheating time.<br><br>* Supports configuration of route priority. |No |
|1.0.0 |2024\-02\-08 |Supports log delivery, allowing logs to be delivered to Log Service TLS for persistent storage. |No |


<span id="3NHRTgmL"></span>
## View version


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig), and in the top navigation bar, select the target region.

2. Select **Instance Management** in the navigation bar on the left. In the instance list, you can view the version information of gateway instances.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84c48f28ef34441431cc6ebbf28efe28.png) </span>

<span id="rpCQZV5X"></span>
## Upgrade version

All instances created after a new version is released are set to the latest version by default.

Currently, upgrading instance versions by yourself is not supported for existing older version instances. If you need to upgrade, please [submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000170&FlowKey=DhvSFwiOSXyEVSlGZJXx) for processing.
