---
title: "What is PrivateLink"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01"
---

<span id=".566A5LuL"></span>
## Overview

PrivateLink establishes private network connections through endpoints and endpoint services, enabling different VPCs to privately access service resources. This avoids the potential security risks of internet access, providing you with a more secure networking solution.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f688b38867628b1d79f293132dfcc663.png) </span>

<span id=".5Z-65pys57uE5oiQ"></span>
## Basic components

PrivateLink service primarily consists of three components: Endpoint Service, Endpoint, and Endpoint Connection, involving both a Service Provider and a Service Consumer.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a46ef33e53de83fcbf9d15a4c82cc0cb.png) </span>

Detailed descriptions of each component are as follows:


|Compositions |Description |
|---|---|
|End point node |An endpoint serves as the entry point within the service consumer's VPC to connect to an endpoint service. It can be associated with the service provider's endpoint service. A single endpoint can only be associated with one endpoint service. However, different endpoints can be associated with the same endpoint service, establishing a many\-to\-one relationship between endpoints and an endpoint service.<br><br><br>* **Endpoint network interface**: Refers to the elastic network interface (ENI) automatically created by the system when an endpoint is established. It serves as the entry point for the endpoint to access the endpoint service. Each endpoint can have only one ENI per Availability Zone. ENIs cannot be shared across different Availability Zones.<br><br>* **Endpoint security group**: An endpoint must be associated with at least one security group by default. This security group controls the inbound and outbound traffic to the endpoint ENI. |
|Endpoint Service |Endpoint service refers to a service that can establish private connections with other VPCs through endpoints. It is created and managed by the service provider.<br><br><br>* **Service resource**: The resource that provides services to an endpoint. Supported types include: Classic Load Balancer (CLB), Application Load Balancer (ALB).<br><br>* **Allowlist**: Controls which accounts can access service resources via the endpoint service.<br><br><br>Endpoints within the same account can access the endpoint service without being added to the allowlist. For endpoints from different accounts to access the endpoint service, you must add the endpoint's account ID to the service allowlist of the endpoint service. |
|Endpoint connection |Endpoint connection: A unidirectional, private network connection established between an endpoint and an endpoint service. |


<span id=".6K6_6Zeu5pa55byP"></span>
## Access methods


* **Console access**

   You can manage these resources directly via the web console by logging into either the Endpoint console or the Endpoint Service console.

* **API access**

   You can use either HTTP or HTTPS to request online API calls or custom development. For details, see [API reference](https://docs.byteplus.com/en/docs/privatelink/Overview).
