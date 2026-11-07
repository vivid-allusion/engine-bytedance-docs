---
title: "Configure traffic mirroring policy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Configure_traffic_mirroring_policy"
---

Traffic mirroring is the capability to replicate API request traffic in real time and forward it to a specified mirror backend. After traffic mirroring is enabled, APIG forwards requests to the original backend as usual, and simultaneously copies the same requests to the mirror backend. The mirror backend's response is not returned to the client. This article describes how to configure a traffic mirroring policy in an APIG route.

<span id="WRvGCCiM"></span>
## Application scenario

In a microservice architecture, applications iterate frequently. Traditional test environments cannot fully simulate the characteristics of production traffic, and direct canary release in the production environment carries risks. The traffic mirroring capability addresses this issue. It is suitable for scenarios such as new version service validation, fault diagnosis, security audit, and more, helping you use production traffic for testing and validation without impacting online business.


|**Scenario** |**Description** |**Typical configuration** |
|---|---|---|
|New version service validation |Copy production traffic to the new version service to validate its processing capability and business logic correctness without impacting online users. |* Original backend: v1.0 production service<br><br>* Image backend: v2.0 test service<br><br>* Image ratio: 50% |
|Database migration validation |Send identical query requests simultaneously to both the old and new databases, compare the response results, and ensure data consistency and that query performance meets the required standards. |* Original backend: MySQL Service<br><br>* Image backend: TiDB Service<br><br>* Image ratio: 100% |
|Security audit and risk control |Mirror all traffic to the security analysis service for real\-time threat detection and behavior analysis without impacting the primary business path. |* Original backend: Business Service<br><br>* Image backend: Security audit service<br><br>* Image ratio: 100% |


<span id="j6cFhTVY"></span>
## Prerequisites


* A route has been created. For details, see [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* The original backend service (Upstream) and mirror backend have been created. For details, see [Upstream Management](https://docs.byteplus.com/en/docs/apig/Upstream_Management).


<span id="0jsslJ6W"></span>
## Procedure


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. Select the target instance from the ** Instance management** drop\-down list, and then click **Route list**. 

4. In the route list, locate the target route and click **Edit** in the **Actions** column.

5. On the edit route page, in the **Advanced settings** area, check **traffic mirroring** and then **enable**, and configure the mirror backend.

   
   |Parameter |Description |
   |---|---|
   |Upstream types |Select the type of image backend service. |
   |Select upstream |Select the created image backend service. |
   |Image ratio |Enter the traffic ratio to be copied to the mirror backend. |
   

6. Click **Confirm**.


<span id="RGSiIrDM"></span>
## Validate the result

After the configuration is complete, send a request to the route to verify the result. Requests matching the route are forwarded to the original backend, and are also copied and sent to the mirror backend according to the configured mirroring ratio (for example, 40%).
