---
title: "Cloud server type Upstream"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Elastic_Compute_Service_type_Upstream"
---

API Gateway supports connecting to BytePlus ECS cloud servers, abstracting multiple cloud servers into a single Upstream, which serves as the gateway's routing backend. Applicable to scenarios where the business is deployed on ECS and needs to be released through a gateway. This article explains how to create an ECS\-type Upstream.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The API Gateway instance has already been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* ECS has been purchased, and business deployment is complete. For details, refer to [Purchase a cloud server](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Upstream is an instance\-level resource. Within the same Instance, the same Upstream can only be created once.

* API Gateway instance and ECS instance must be located within the same VPC.

* An Upstream can be associated with up to 20 ECS, and each ECS can be configured with up to 5 access ports.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance in **Instance Management**, click the **Upstream list**.

4. On the Upstream list page, click **Create Upstream**.

5. On the Create Upstream page, fill in the parameter information as required.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Upstream name |Customize Upstream name Within the same Instance, the Upstream Name is unique. |
      

   * **Backend configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Choose the backend service type that Upstream connects to. In this scene, choose **cloud server**.<br><br><br>* **Add cloud server**: Click **Add server**, and the **Add server** configuration interface will appear. Check the target ECS Name.<br><br>* **Configure port**: Click **Next** to configure the access port for each ECS instance. API Gateway can only access the corresponding ECS through the configured port.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only ECS instances whose status is Running can be selected.</div><br> |
      |Protocol |Choose a protocol type. Support **HTTP1.1**, **HTTP2**, and **HTTP2/GRPC**. |
      |TLS settings |Configure TLS.<br><br><br>* **Disable TLS**: The gateway accesses the Backend Upstream using the HTTP protocol.<br><br>* **One\-way TLS**: The gateway accesses the Backend Upstream using the HTTPS protocol, and the corresponding certificate must be selected. |
      |Load balancing algorithm |Configure the load balancing algorithm.<br><br><br>* **Polling**: (Default) Distributes all requests sequentially to each ECS. This method is suitable for scenarios in which the ECS hardware configuration is identical.<br><br>* **Random**: Request random allocation to each ECS.<br><br>* **Least connections**: Allocate requests to the ECS with the fewest active requests.<br><br>* **Consistent hashing**: Load balancing based on header/querystring information ensures that, when the number of backend services remains unchanged, users carrying the same information can consistently access the same ECS. Support click **Enable Overload Protection**, set **Load Threshold**, and enable instance overload protection. Once enabled, if an instance's active request count exceeds the threshold based on the average active request count, the instance will not be selected, even if the hash value matches that instance. |
      |Service circuit breaking |Whether circuit breaking is enabled in configuration.<br><br>Once this feature is enabled, API Gateway can improve the routing hit rate by configuring circuit breakers without consuming additional traffic. For details, see [Circuit breaking policies](https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy). |
      |Warm up time |When the load balancing algorithm is configured to use **Round robin** or **Least connections**, it can be configured.<br><br>Configure the warm\-up time for the backend service. Must be an integer, with a value range from 1 up to but not including 10000; the unit is seconds (s). |
      

6. Click **Confirm**.


<span id=".5pS-6KGMIEFQSUcg5a6J5YWo57uE"></span>
## Security group configuration

You need to allow the APIG security group (named `apig-sg-<accountID>`) through the corresponding ECS port to ensure that the gateway can access the resources on that port.

For example: Suppose you set the ECS access port to 8080. Log in to the cloud server console, select the security group associated with the main network interface card of the target ECS instance, and add an inbound rule to allow traffic from the APIG security group on port 8080.


&nbsp;


&nbsp;
