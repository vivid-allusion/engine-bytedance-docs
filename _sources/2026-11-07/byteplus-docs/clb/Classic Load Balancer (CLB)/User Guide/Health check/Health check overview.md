---
title: "Health check overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Health-check-01"
---

<span id=".5qaC6L-w"></span>
## Overview

CLB can determine whether the backend server status is healthy, stop forwarding requests to unhealthy backend servers, and ensure overall service availability.

CLB supports configuration of health checks based on the listener dimension. When [creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener), you can configure health checks.

<div data-tips="true" data-tips-type="warning">warning</div>


<div data-tips="true" data-tips-type="warning">Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload. However, to ensure the continuous availability of the business, you are not advised to disable the health check feature. Otherwise, the listener may forward requests to abnormal backend servers.</div>


<span id="44itdkO3"></span>
## classification

Classified based on the protocol used by health checks, as shown in the table below:


|Health check protocol |Explaination |Applicable scenarios |
|---|---|---|
|TCP |Send SYN handshake packets to verify the status of the backend server port. |Only TCP listeners can be used. |
|UDP |Send ICMP or UDP probe packets to detect whether the backend server is functioning properly. |Only UDP listeners can be used. |
|HTTP |Send HEAD or GET requests to simulate browsing behavior and check if the application of the backend server is functioning properly. |Only HTTP/HTTPS listeners can be used. |


<span id="44itdkO3"></span>
## Status and health check time


* **Stage**

   
   |Stage |Explaination |
   |---|---|
   |Normal |All servers within the backend server group attached to the listener function properly. |
   |Abnormal |The backend server group associated with the listener contains server exceptions. |
   |Disabled |The listener has not enabled the health check. |
   |No target |No Server Group is configured among all backend server groups attached to the listener. |
   

* **Health check time**

   
   |Name |Explaination |Example Value |
   |---|---|---|
   |Response timeout |Waiting time for the health check response.<br><br><br>* If no correct information is received back from the backend server within the response timeout period, the health check is considered failed.<br><br>* Value range: 1 to 60 seconds. The default value is 2s. |2 seconds |
   |Detect interval |Interval between health checks.<br><br><br>* The detection interval must be greater than or equal to the response timeout.<br><br>* The value ranges from 2 seconds to 300 seconds. The default interval is 2 seconds, which means a health check is conducted on the backend server every 2 seconds. |5 seconds |
   |Healthy threshold |The number of health checks to mark a backend server as normal.<br><br><br>* When a specified number of health checks are conducted continuously on the same backend server and all results are successful, its health check status changes from **exception** to **normal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   |Unhealthy threshold |The number of health checks to mark a backend server as unhealthy.<br><br><br>* When a specified number of consecutive health checks are conducted on the same backend server and all results fail, its health check status changes from **Normal** to **Abnormal**.<br><br>* The value range is from 2 to 10 times. The default value is 3 times. |3 |
   

* **Check process**

   Demonstrate the health check process based on the **health check time** table's example.

   
   <Tabs>
   <Tab zoneid="EQaK0PENV8" title="TCP/UDP protocols">
   <TabTitle>TCP/UDP protocols</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f03fc3086a8085024176450753fef6b.png) </span>
   
   
   
   
   </Tab>
   <Tab zoneid="QY8hefsoxi" title="HTTP">
   <TabTitle>HTTP</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_357ee1d39f1cdf9c14d23ea51d49f029.png) </span>
   
   
   </Tab>
   </Tabs>
   


<span id="6Qww8SqG"></span>
## Implementation Mechanism


<Tabs>
<Tab zoneid="LKpvMayLom" title="TCP">
<TabTitle>TCP</TabTitle>

The TCP listener uses the TCP protocol to perform health checks on backend server groups.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a05528b84131da968b12951b34c0d8b.png) </span>

The implementation mechanism of the TCP listener health check is as follows:


1. The CLB instance sends a TCP SYN packet to the private IP and port of the backend server based on the health check configuration of the listener.

2. After the backend server receives the request, if the corresponding port is listening normally, the server returns a SYN+ACK packet.

3. If the CLB instance fails to receive a data packet back from the backend server within the **timeout period**, it considers the service unresponsive, determines the health check has failed, and sends an RST packet to release the TCP connection.

4. If the CLB instance successfully receives a data packet back from the backend server within the **timeout period**, it considers the service is running normally, determines the health check has succeeded, and then sends an RST packet to release the TCP connection.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a normal TCP 3\-way handshake, after the CLB instance receives a SYN+ACK packet from the backend server, it further sends the ACK packet and then transmits data. However, if the health check is enabled, the CLB instance immediately sends an RST packet to release the TCP connection.</div>


<div data-tips="true" data-tips-type="tip">This implementation mechanism may cause the backend server to consider the related TCP connection to have exited with an exception and throw an error message, such as <code>Connection reset by peer</code>. The solution is as follows:</div>



* <div data-tips="true" data-tips-type="tip">Use HTTP for health checks.</div>


* <div data-tips="true" data-tips-type="tip">If the real IP address of the client is configured on the backend server, connection errors from the health check can be ignored.</div>



</Tab>
<Tab zoneid="yR8bRq78ph" title="UDP">
<TabTitle>UDP</TabTitle>

The UDP listener uses the UDP protocol to perform health checks on backend server groups. The implementation mechanism varies slightly depending on whether the health check string is specified, as shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5d14a9a3bf9842d21be578b9e4c505d.png) </span>


&nbsp;

* When no health check string is specified, the implementation mechanism of UDP listener health check is as follows:

   1. The CLB instance sends an ICMP packet to the private IP address of the backend server.

   2. The CLB instance sends a UDP detection packet to the private IP address and health check port of the backend server.

   3. If within the **response timeout period**, the ICMP packet is sent successfully and the CLB instance does not receive an error message such as `port unreachable` from the backend server, the health check is deemed successful; otherwise, it is deemed a failure.

* When the health check string is specified, the implementation mechanism of the UDP listener health check is as follows:

   1. The CLB instance sends a UDP detection packet to the private IP address and health check port of the backend server based on the specified health check string.

   2. If the CLB instance receives the expected information from the backend server before the **response timeout period** expires, the health check is successful. Otherwise, the health check fails.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The UDP listener health check may result in a situation where the health check status does not match the actual service status.</div>


* <div data-tips="true" data-tips-type="tip">When the operating system of the backend server is Linux, its anti\-ICMP attack mechanism limits the speed of sending ICMPs in high concurrency scenarios, and abnormal backend servers cannot return error messages in a timely manner. As a result, the listener may misjudge that the health check is successful.</div>



</Tab>
<Tab zoneid="miTw51SQvH" title="HTTP">
<TabTitle>HTTP</TabTitle>

The HTTP/HTTPS listener uses the HTTP protocol to perform health checks on backend server groups.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c78736fd4312525a06812adf1efd1ab.png) </span>

The implementation mechanism is as follows:


1. The CLB instance sends an HTTP GET/HEAD request to either the (private IP + port + URL) or (domain name + URL) of the backend server based on the health check configuration of the listener.

2. After receiving the request, the backend server returns an HTTP status code based on the running status of the corresponding service.

3. If the CLB instance does not receive any information from the **backend server** before the response timeout expires, it determines that the service is not responding and the health check fails.

4. If the CLB instance successfully receives the information from the backend server before the **response timeout** expires, it compares the returned HTTP status code with the configured status code. If the two codes are consistent, the health check is successful.


</Tab>
</Tabs>
