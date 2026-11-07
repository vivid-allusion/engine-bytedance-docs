---
title: "Endpoint service overview"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Overview-endpoint-services"
---

<span id=".566A5LuL"></span>
## Overview

Service providers use Endpoint Services to allow service consumers to connect.

<span id="lgceGo5Z"></span>
## Classification

PrivateLink supports the following two types of Endpoint Services:


* **Normal Endpoint Service**: Created and managed by user accounts as service providers, with default names automatically generated in the format **com.volces.privatelink.**  ** *<RegionID\>* **  **.**  ** *<EndpointServiceID\>* ** .

   Currently supported service resources are: Classic Load Balancer (CLB), Application Load Balancer (ALB), Network Load Balancer (NLB). Before manually creating an Endpoint Service, you need to prepare the service resources. For detailed configuration, see [CLB Getting Started](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-01), [ALB Getting Started](https://docs.byteplus.com/en/docs/clb/ALB-quick-start-Overview), [NLB Getting Started](https://docs.byteplus.com/en/docs/clb/NLB-Quick-start).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5dd7a9260387de24dc6efeedc391b2fb.png) </span>



&nbsp;

* **BytePlus** ** Service**: These are created and managed by official BytePlus  services (e.g., Torch Object Storage (TOS)) as the service provider. The service name is fixed and cannot be changed. 


<span id=".57uI56uv6IqC54K55pyN5Yqh5bim5a69"></span>
## Endpoint service bandwidth

The bandwidth of an Endpoint Service varies depending on its service type.


* When the endpoint service is a BytePlus service, its bandwidth is determined by the official specifications of that service. To adjust the bandwidth, see corresponding product documentation.

* When the Endpoint Service is a normal service, its bandwidth is limited by the service resource and is the lower value between the bandwidth of the CLB/ALB/NLB instance and the bandwidth of the backend servers.

   * To adjust the CLB instance bandwidth, see [Modifying a CLB instance type](https://docs.byteplus.com/en/docs/clb/CLB-instances-03).

   * To adjust the backend server bandwidth, see [Modifying an ECS instance type](https://docs.byteplus.com/en/docs/ecs/Overview-2).

   * The bandwidth of ALB instances, NLB instances cannot be adjusted.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The PrivateLink support for ALB, NLB service resources is in beta stage. For trial requests, contact your account manager.   </div>
   

<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures

The configuration process for the endpoint service is shown below.


1. [Create endpoint service](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services): Create an endpoint service instance, select the Load Balancer resource that provides the service.

2. [Add allowlist](https://docs.byteplus.com/en/docs/privatelink/Managing-allowlists-for-endpoint-services#.5re75Yqg5pyN5Yqh55m95ZCN5Y2V): Grant account authorization for cross\-account endpoints, enabling them to access this endpoint service. Configuration of this step is not required when accessing from an endpoint in the same account.

3. View endpoint service: Check the status of the Endpoint Service and the status of endpoint connections established on it to confirm successful configuration.
