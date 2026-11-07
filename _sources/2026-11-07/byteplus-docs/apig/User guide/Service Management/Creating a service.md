---
title: "Creating a service"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_a_service"
---

Service is a set of Ingress exposed to the external, used to distinguish the source and protocol of traffic, achieving business, environmental, and logical tenant isolation. Service can bind an independent domain name, accessing business through the dimension of domain name. This article explains how to create a service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An AIPG Instance has been created. For details please refer to [Creating an Instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

<span id=".5Yib5bu65pyN5Yqh"></span>
## Creating a Service


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. Select **Route management \> Service list (Domain name)**  from the left navigation bar. Click **create service**.

4. In the create service dialog, set the service parameters.



|Parameter |Description |
|---|---|
|Instance |Service belongs to instance\-level resources, please select the instance currently associated with the service. |
|Service name |Customize the Service name. The Service name must be unique under the same instance. |
|Notes/comments |Enter notes/comments. |



5. Click **Confirm** to complete the creation of the service.
