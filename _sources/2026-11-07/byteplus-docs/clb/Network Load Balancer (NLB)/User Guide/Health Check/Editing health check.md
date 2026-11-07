---
title: "Editing health check"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Editing-health-check"
---

<span id="oilGveoQ"></span>
## Prerequisites

The security group attached to network interface of the Elastic Compute Service (ECS) has allowed the health check traffic. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL)

<span id="sXoo8aii"></span>
## Procedure


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left\-side navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and target region.

4. On the right side of the target server group, choose **Edit health check**.

5. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Sample Value |
   |---|---|---|
   |Health Check |Select whether to enable the health check feature. After enabling health checks, NLB can check whether the backend server status is normal, stop forwarding requests to abnormal backend servers, and ensure overall service availability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Disabling health checks may result in requests being forwarded to abnormal backend servers. To ensure continuous availability of the service, it is discouraged to disable health checks.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload.</div><br> |Enable  |
   |Health check protocol |The protocol type of the health check request.<br><br><br>* **TCP**: Sends SYN handshake messages to detect whether the backend server port's status is normal.<br><br>* **HTTP**: Sends HEAD or GET requests to simulate browsing behavior, thereby detecting whether the backend server application is functioning normally. HTTP\-specific argument details are as follows:<br><br>   * **Health check method**: Select the request method for performing a health check on the backend server.<br><br>      * **GET**: GET request responses return both the response header and response body, requiring server support for the GET method.<br><br>      * **HEAD**: HEAD request responses only return the response header information, reducing backend overhead. Support for the HEAD method is required on the server.<br><br>   * **Health check domain name**: Input the domain name of the health check request, which must be set to the actual externally\-facing address provided on the backend server. If not specified, the default backend server private IP address will be used.<br><br>   * **Health check path**: Input the URL of the health check request path, which must be set to the actual externally\-facing address provided on the backend server. If not specified, it defaults to`/`.<br><br>   * **Healthy status code**: Configure response code. If the response code of the selected type is received, the server is considered available.<br><br>* **UDP**: Sends ICMP or UDP probing packets to detect whether the backend server is operating normally. Specific arguments for UDP protocol are as follows:<br><br><br> **  ** Custom request/response: Enable or disable the switch for specifying health check characters.<br><br><br>   * Once enabled, configure the following parameters:<br><br>      * **Custom request**: input the character for the health check request.<br><br>      * **Custom response**: input the character for the health check response.<br><br>   * When disabled, specifying a character is unnecessary.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the backend protocol of the server group is TCP, health check does not support the UDP protocol.</div><br> |TCP |
   |Health check port number |Configure the port used for the health check.<br><br><br>* **Use the backend server port**: Health checks are performed on the backend server's port by default, with no need to specify an additional port.<br><br>* **Specify a specific port**: This option is mandatory when the all\-port forwarding feature is enabled. Value range for port: 1 to 65535. |Use backend server port. |
   |Response timeout |Configure the waiting time for the health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* The value range is 1 to 60 seconds. The default timeout period is 3 seconds. |3 seconds |
   |Detect interval |Input the interval for executing the health check.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* The value ranges from 3 seconds to 300 seconds. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. |10 seconds |
   |Healthy threshold |Input the number of health checks to mark the backend server as normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **normal**, its status changes from **abnormal** to **normal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   |Unhealthy threshold |Input the number of health checks to determine backend server exceptions<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **abnormal**, its status changes from **normal** to **abnormal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   


<span id="RJ5GO28h"></span>
## Related document

[ModifyNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBServerGroupAttributes)
