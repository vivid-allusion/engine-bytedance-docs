---
title: "Upstream function service type"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Function_services_type_Upstream"
---

API Gateway supports connecting to BytePlus function services (veFaaS), abstracts a published function as an Upstream, which serves as the backend for gateway routing. Applicable to scenarios where businesses adopt veFaaS deployment and wish to release through the gateway. This article explains how to create a veFaaS\-type Upstream.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The API Gateway instance has been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The function has been created and released. For details on specific operations, refer to [Create Function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection) and [Release Function](https://docs.byteplus.com/en/docs/faas/Release_function).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* The API Gateway instance and veFaaS function must be in the same region.

* Upstream is an instance\-level resource. Within the same instance, the same Upstream can only be created once.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance in **Instance Management**, click **Upstream list**.

4. On the Upstream list page, click **Create Upstream**.

5. On the Create Upstream page, fill in the parameter information as required.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Upstream name |Custom upstream name. Within the same Instance, the Upstream Name must be unique. |
      

   * **Backend configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Choose the backend service type that Upstream connects to. This scenario uses **function services**.<br><br>**Function**: Choose the target function to connect to Upstream.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only released functions can be used as the routing backend for API Gateway.</div><br> |
      

6. Click **Confirm**.
