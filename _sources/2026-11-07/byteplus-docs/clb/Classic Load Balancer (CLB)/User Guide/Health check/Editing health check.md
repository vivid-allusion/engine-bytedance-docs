---
title: "Editing health check"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Editing-health-check"
---

<span id="u0W1hEna"></span>
## Prerequisites

The security group attached to the Elastic Compute Service (ECS) has allowed the traffic for the health check. [Learn more](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group)

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="dF1t8J8U7U" title="TCP listener">
<TabTitle>TCP listener</TabTitle>

1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the region and project.

3. Click **Configure Listener** to the right of the target CLB instance.

4. On the right side of the target listener, click  **···**  ** \> Edit health check**.

5. Refer to the table below for configuration related arguments.

   
   |**Name** |**Explaination** |**Sample Values** |
   |---|---|---|
   |Health Check |Check whether the health check feature is enabled. Once enabled, the CLB instance periodically sends requests to the backend server to test its running status and determine if it is available. When a backend server is found unhealthy, the listener stops sending traffic to this server and forwards the traffic to other backend servers that run normally. |Enable |
   |Response timeout |Enable health check and input the time for waiting for the health check response.<br><br><br>* If no correct information is received back from the backend server within the response timeout period, the health check is considered failed.<br><br>* Value range: 1 to 60 seconds. The default value is 2s. |2 seconds |
   |Detect interval |Enable health check, then input the interval between health checks.<br><br><br>* The detection interval must be greater than or equal to the response timeout.<br><br>* The value ranges from 2 seconds to 300 seconds. The default interval is 2 seconds, which means a health check is conducted on the backend server every 2 seconds. |2 seconds |
   |Healthy threshold |Enable health check, then input the number of health checks to determine that the backend server is normal.<br><br><br>* Value range: 2–10 times. The default value is 3 times. |3 |
   |Unhealthy threshold |Enable health check, then input the number of health checks to determine backend server exception.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are abnormal, its status changes from **Normal** to **Abnormal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   

6. Click **Confirm** button to complete the actions.


</Tab>
<Tab zoneid="Be1Tcl0sV5" title="UDP listener">
<TabTitle>UDP listener</TabTitle>

1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target project and target region.

3. Click **Configure Listener** to the right of the target CLB instance.

4. On the right side of the target listener, click  **···**  ** \> Edit health check**.

5. Refer to the table below for configuration related arguments.

   
   |**Name** |**Explaination** |**Sample Values** |
   |---|---|---|
   |Health Check |Check whether the health check feature is enabled. Once enabled, the CLB instance periodically sends requests to the backend server to test its running status and determine if it is available. When a backend server is found unhealthy, the listener stops sending traffic to this server and forwards the traffic to other backend servers that run normally. |Enable |
   |Health check request |Specify the request string sent for a health check. |healthcheckrequest |
   |Expect the correct response |Response string expected to be returned when the health check result is normal.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If <strong>Health Check Request</strong> is specified, you must configure this parameter.</div><br> |ok |
   |Response timeout |After enabling health check, input the time to wait for a health check response.<br><br><br>* If no correct information is received back from the backend server within the response timeout period, the health check is considered failed.<br><br>* Value range: 1 to 60 seconds. The default value is 2s. |2 seconds |
   |Detect interval |Enable health check, then input the interval between health checks.<br><br><br>* The detection interval must be greater than or equal to the response timeout.<br><br>* The value ranges from 2 seconds to 300 seconds. The default interval is 2 seconds, which means a health check is conducted on the backend server every 2 seconds. |2 seconds |
   |Healthy threshold |Enable health check, then input the number of health checks to determine that the backend server is normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are normal, its status changes from **Abnormal** to **Normal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   |Unhealthy threshold |After enabling health check, input the number of health check attempts to determine exceptions of the backend server.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are abnormal, its status changes from **Normal** to **Abnormal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   

6. Click **Confirm** button to complete the actions.


</Tab>
<Tab zoneid="mFs2BgLHZT" title="HTTP/HTTPS listener">
<TabTitle>HTTP/HTTPS listener</TabTitle>

1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target project and target region.

3. Click **Configure Listener** to the right of the target CLB instance.

4. On the right side of the target listener, click  **···**  ** \> Edit health check**.

5. Refer to the table below for configuration related arguments.

   
   |**Name** |**Explaination** |**Sample Value** |
   |---|---|---|
   |Health Check |Check whether the health check feature is enabled. Once enabled, the CLB instance periodically sends requests to the backend server to test its running status and determine if it is available. When a backend server is found unhealthy, the listener stops sending traffic to this server and forwards the traffic to other backend servers that run normally. |Enable |
   |Health check method |After enabling the health check, select the request method for the health check of the backend server, supporting GET or HEAD.<br><br><br>* HEAD: The server only returns the HEAD header information, which can reduce backend overhead but requires the server to support the HEAD method.<br><br>* GET: Requires the server to support the GET method. |HEAD |
   |Health check domain name |After enabling health check, input the domain name of the health check request, that is, Host. This parameter must be set to the real address of the backend server that provides services for entities beyond the local VPC.<br><br><br>* If this parameter is not specified, the private IP address of each server in the backend server group is used by default, and Host is left empty.<br><br>* Host specifies the IP address of the backend server to be accessed by the client or the domain name of the specific service on the server. When there are multiple services on the backend server, the client can distinguish and access different services based on Host. |www.test.com |
   |Health check path |After enabling the health check, input the request path URL for the health check, which should be configured as the address that the backend server publicly provides services on. If not specified, it defaults to`/`. |/ |
   |Normal status code |Enable health check and select the normal status code.<br><br><br>* If a response code of the selected type is received, the server is in a normal state.<br><br>* Supports 2XX, 3XX, 4XX, and 5XX. |2XX, 3XX |
   |Response timeout |Enable health check and input the time for waiting for the health check response.<br><br><br>* If no correct information is received back from the backend server within the response timeout period, the health check is considered failed.<br><br>* Value range: 1 to 60 seconds. The default value is 2s. |2 seconds |
   |Detect interval |After enabling the health check, input the interval for executing the health check.<br><br><br>* The detection interval must be greater than or equal to the response timeout.<br><br>* The value ranges from 2 seconds to 300 seconds. The default interval is 2 seconds, which means a health check is conducted on the backend server every 2 seconds. |2 seconds |
   |Healthy threshold |Enable health check, then input the number of health checks to determine that the backend server is normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are normal, its status changes from **Abnormal** to **Normal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   |Unhealthy threshold |Enable health check, then input the number of health checks to determine backend server exception.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are abnormal, its status changes from **Normal** to **Abnormal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   

6. Click **Confirm** to complete the actions.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes)
