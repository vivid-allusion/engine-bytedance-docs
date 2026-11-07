---
title: "Quick guide"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Quick_guide"
---

This document is intended to help you understand the basic usage process of the API gateway and get started quickly.

<span id=".5L2_55So5rWB56iL"></span>
## The main process:

The usage process of the API gateway is shown in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ed9dc1bdf521ffe017c90fa69558b67.png) </span>


1. Register a BytePlus account and activate console permission for the API Gateway.

2. Create an APIG instance. For specific operations, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

3. Create a service.

   A Service is a set of routes that provide external entry points, used to distinguish traffic sources and protocols, and to achieve isolation of business, environment, and logical tenants. Supports binding custom domain names in a Service. For specific operations, refer to [Service management](https://docs.byteplus.com/en/docs/apig/Service_Management).

4. (Optional) Import external resources.

   If a service is deployed in a VKE cluster or managed using the MSE registration center, you must import the external resources used by the service in advance so that the API gateway can obtain the resource list, including:

   * [Import container clusters](https://docs.byteplus.com/en/docs/apig/Import_container_cluster)

5. Create an Upstream.

   The API gateway abstracts backend services with the same functionality into a single Upstream, enabling decoupling of routing and backend services. Provide more flexible support for backend application scenarios such as canary release and multi\-version management. It supports multiple forms of Upstream backends, including:

   * [VKE type Upstream](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream)

   * [Function Service type Upstream](https://docs.byteplus.com/en/docs/apig/Function_services_type_Upstream)

   * [Elastic Compute Service upstream type](https://docs.byteplus.com/en/docs/apig/Elastic_Compute_Service_type_Upstream)

   * [Fixed domain name type: Upstream](https://docs.byteplus.com/en/docs/apig/Fixed_domain_name_type_Upstream)

   * [Upstream with fixed IP type](https://docs.byteplus.com/en/docs/apig/Fixed_IP_type_Upstream)

6. Add route.

   By using the add route feature, requests that meet specified rules can be distributed to multiple target upstreams according to the configured traffic weight, supporting scenarios such as multi\-version management for applications. For specific operations, refer to [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

   Also supports configuration of multiple routing policies, including:

   * [Timeout policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy)

   * [Cross-domain policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_cross-origin_policy)

   * [Rewrite policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_rewrite_policy)

   * [Retry policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_retry_policy)

7. Consumer management.

   A consumer is an abstraction of objects that access the API gateway. By using consumers, the gateway can merge one or more objects into a single user identity, making it easier to control permissions and manage users based on the source of access. A consumer can be any of various client applications, mobile applications, web applications, third\-party services, or other systems. For specific operations, refer to [Create a consumer](https://docs.byteplus.com/en/docs/apig/Creating_a_consumer).


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After connecting backend services to the API gateway. You can further debug your Service using API debugging tools such as Postman to verify whether your Service can properly provide services to external users.
