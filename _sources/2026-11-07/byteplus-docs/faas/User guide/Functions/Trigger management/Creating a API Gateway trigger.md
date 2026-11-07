---
title: "Creating a API Gateway trigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_a_API_Gateway_trigger"
---

FaaS supports using BytePlus API Gateway as the event source, triggering function logic through public or private network HTTP/HTTPS traffic, and providing the functional capabilities to external users. This article introduces how to create an API Gateway trigger.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">API Gateway Service and API Gateway trigger are in <strong>beta</strong>. To use them, contact your BytePlus costomer manager.</div>


<span id="background-information"></span>
## Background Information

API Gateway triggers are bidirectional integration triggers, supporting configurations via both the FaaS console and the API Gateway console. Correspondences are as follows:

On the FaaS side, the API Gateway trigger corresponds to a function type Upstream and a set of routes pointing to the current Upstream.

<span id="prerequisites"></span>
## Prerequisites


* The function must have been fully released at least once. For detailed operations, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

* An API Gateway instance and service have been created.


<span id="usage-limit"></span>
## Usage limit


* A maximum of 20 triggers can be created for each function.

* On the FaaS side, under the same gateway instance, a function only supports creating one API Gateway trigger; moreover, an API Gateway trigger only supports binding one route with 100% weight.

* Once an API Gateway trigger is created, it does not support changing the owning gateway instance and gateway service, nor modifying the trigger name and route name.

* Each API Gateway trigger can display up to five gateway services and 200 routes. If exceeded, you will need to check the API Gateway Console.

* Before deleting a function, you must first delete all API Gateway triggers.

* Recommended entry point

   * If you only need one route with 100% going to the target function, it is recommended to create an API Gateway trigger on the FaaS side. In this situation, the FaaS side supports create/edit/delete operations.

   * If you have additional requirements, such as a route that connects to multiple functions for multi\-version/environment management, or multiple routes connecting to one function, go to [API Gateway console](https://console.byteplus.com/veapig) for operations. In this scenario, the function service side only supports viewing bound route information and does not support create/edit/delete operations.


<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Functiont** page, find the function for which you need to create a trigger and click its name.

4. In the function details page, under the **Triggers** tab, click **Create trigger**.

5. In the **Create trigger** panel, set the parameters as required.

   * Basic settings

   
   |Parameter |Description |
   |---|---|
   |Trigger type |This scenario selects the API Gateway trigger. |
   |Trigger name |Custom trigger name. Under the same function, trigger names cannot be duplicated. Trigger names cannot be modified after being successfully created. |
   |Gateway instance |Select the gateway instance that the trigger belongs to. |
   |Gateway service |Select the gateway service that the trigger belongs to further. |
   

   * Gateway route

      Bind a 100% weight route to the current API Gateway trigger.

   
   |Parameter |Description |
   |---|---|
   |Route name |Customize the route name. The route name cannot be modified once it has been successfully created. |
   |Path |Set the request paths that are allowed to access the function. Only supports prefix matching; the path must start with "/"`/`beginning. |
   |Weight |Displays the traffic weight of the current route. FaaS side only supports configuring routes with 100% weight. |
   |Request method |Select the request methods that are allowed to access the function. Supports 6 types of request methods: POST, GET, PUT, DELETE, HEAD, OPTIONS. Please choose as needed. |
   |Timeout |The API gateway trigger forwards the request to the function and waits for the function to respond within a maximum time limit. After turning on the switch, you must set a specific timeout period. Please choose whether to enable it based on your actual needs.<br><br><br>* Turning on the timeout switch allows separate control of the request timeout for the API gateway trigger. If you have also set the timeout for this function on the FaaS side, the effective timeout will be the smaller of the two.<br><br>* If the timeout switch is off, then the API gateway trigger has no timeout limit. |
   |Cross\-domain switch |Enable cross\-domain access by adding `Access-Control-Allow-Origin: *` to the response headers. If your function allows cross\-domain access, enable the cross\-domain switch to ensure secure transmission of cross\-domain data. |
   

6. Click **Confirm** to complete the creation of the API gateway trigger.


<span id="what-to-do-next"></span>
## What to do next


* If you need to modify the API gateway trigger, refer to [Managing triggers](https://docs.byteplus.com/en/docs/faas/Managing_triggers).

* If you need to monitor the operational status of the function, refer to [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs).
