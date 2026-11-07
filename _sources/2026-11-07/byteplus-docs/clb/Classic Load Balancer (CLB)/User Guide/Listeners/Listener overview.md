---
title: "Listener overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Listeners-01"
---

<span id=".55uR5ZCs5Zmo55qE5L2c55So"></span>
## Overview

The listener is responsible for monitoring the user access requests received by the CLB instance based on the specified protocol and port. CLB forwards access requests to healthy backend servers within the configured Server Group of the listener using the scheduling algorithm.

CLB supports configuration of the scheduling algorithm and health check at the listener dimension.


* Scheduling algorithm: Used to evenly distribute access requests to backend servers, avoiding situations where one server is overloaded while others are idle. See details below.

* CLB can determine whether the backend server status is healthy, stop forwarding requests to unhealthy backend servers, and ensure overall service availability. [Learn more](https://docs.byteplus.com/en/docs/clb/Health-check-01)


<span id="7MIZsDKG"></span>
## Protocol and port


* **Listening protocol**

   
   |Term |Explaination |Application scenario |
   |---|---|---|
   |TCP |* A connection\-oriented and reliable protocol that must establish a connection with the peer through the 3\-way handshake before packets are formally transmitted and received<br><br>* Data transmission is fast. |* Applicable to scenarios that require high reliability and high data accuracy, and have relatively low speed requirements, such as file transfer, email sending and receiving, and remote login<br><br>* Common web applications |
   |UDP |* Connectionless protocol that does not require a 3\-way handshake with the peer before sending data and sends and receives packets directly without supporting error recovery and data retransmission<br><br>* Reliability is relatively low.<br><br>* Data transmission is fast. |Applicable to scenarios that require real\-time performance and have relatively low requirements for reliability, such as video chatting and real\-time push of financial market updates |
   |HTTP |* Application layer protocol that mainly solves how to package data.<br><br>* Using X\-Forward\-For to obtain the source address |Applicable to applications that require recognition of data content, such as web applications and web games |
   |HTTPS |* Using the SSL protocol to encrypt data transmission to prevent unauthorized access<br><br>* Unified certificate management: You can upload certificates to the CLB instance, with decryption actions completed directly on the CLB instance, reducing CPU overhead on the backend server |Applicable to applications with high security requirements and requiring encrypted transmission |
   

* **Listening port**

   In the same CLB instance, the listening ports for the same protocol must not be duplicated. Listeners support two types of port configurations: listen by single port and full port listening.

   
   |classification |Explaination |Applicable scenarios |
   |---|---|---|
   |Listen by single port |Specify a listening port in the range of 1 ~ 65535. |Applicable for scenarios where all backend servers use the same port to provide external services. |
   |Listening to all ports |Specify the port range for listening ports within the range of 1 ~ 65535 |Suitable for scenarios where a range of consecutive ports is open for backend server applications. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Both HTTP and HTTPS forward traffic over TCP at Layer 3. Therefore, the listening ports for the TCP, HTTP, and HTTPS protocols must be different.   </div>
   

<span id=".6LCD5bqm566X5rOV5Y6f55CG"></span>
## Scheduling algorithm

Supported scheduling algorithms include the following three types:


|Scheduling algorithm |Explaination |Applicable scenarios |
|---|---|---|
|Weighted Round Robin (WRR) |This algorithm distributes access requests from users to different backend servers in sequence based on the weight of each backend server. The better the performance of a server, the higher the weight. A backend server with a higher weight is assigned a larger share of the requests. |Suitable for short connection services. This scheduler is recommended when the processing time of each request on the backend server is basically the same, the types of processed requests are identical or similar, and the request time is similar. |
|Weighted Least Connections (WLC) |First calculate the value of current connections/weight on the backend server, then distribute the requests to the backend server with the smallest value This scheduler needs to record the current number of connections of each server. When a request is distributed to a backend server, its number of connections increases by one. When a request connection is terminated, timed out, or completed on the backend server, its number of connections decreases by one. |WLC is applicable to persistent connection services, such as FTP. This scheduler is recommended when different requests need to be processed and the request time varies significantly. |
|Source IP Hash (SH) |It is the source IP\-based consistent hashing algorithm that distributes requests with the same source IP to the same backend server. When a backend server is removed or added, this schedule can minimize the mapping relationship between existing service requests and request processing servers. |Applicable to protocols without cookie functionality. When requests need to be forwarded from the same user to the same backend server, this scheduler is recommended. |


<span id="cABmod9e"></span>
## Constraints


|Quota |Upper Limit |Changeable? |
|---|---|---|
|Number of forwarding rules that can be added per HTTP or HTTPS listener<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Default forwarding rules are excluded.</div><br> |Please go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CLB) to view |Yes |
|Number of ACLs that can be associated per listener |5 |No |


<span id=".6auY57qn5Yqf6IO95YiX6KGo"></span>
## Advanced feature

The features supported by listeners differ depending on the protocol, as shown in the table below:

> In the table below,  **✓**  indicates support, and  **×**  indicates no support.



|Functionality |Explaination |TCP |UDP |HTTP |HTTPS |
|---|---|---|---|---|---|
|[ACL](https://docs.byteplus.com/en/docs/clb/Access-control-list-01) |Control the listening and forwarding traffic through blocklist or allowlist. | **✓**  | **✓**  | **✓**  | **✓**  |
|[Health Check](https://docs.byteplus.com/en/docs/clb/Health-check-01) |Used to determine whether the backend server's status is normal, preventing requests from being forwarded to servers in an exceptional status and ensuring service availability. | **✓**  | **✓**  | **✓**  | **✓**  |
|[Use of Proxy-Protocol to obtain the source IP](https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-4-listener-to-obtain-the-client-source-IP-address) |When the backend server needs to obtain the real source IP address and the packet source IP is replaced (for example: IPv6 request forwarded to IPv4 backend server), you can enable the Proxy\-Protocol protocol. | **✓**  | **✓**  | **×**  | **×**  |
|Sticky session |Classic Load Balancer will forward the access requests from the same Source IP address to the same backend server for processing. | **✓**  | **✓**  | **✓**  | **✓**  |
|Support for HTTP 2.0 |HTTP 2.0 is a secure and efficient next\-generation HTTP transport protocol, backward compatible with HTTP 1.X protocol versions. If you want the HTTPS service to be more secure, you can enable HTTP 2.0 when configuring the HTTPS protocol listener. | **×**  | **×**  | **×**  | **✓**  |
|Listener bandwidth limit |Enable: The listener exclusively uses the bandwidth of the CLB instance.<br><br>> CLB instances created before April 12, 2023, do not support creating listeners with specified bandwidth. | **✓**  | **✓**  | **✓**  | **✓**  |
|Limit listener New Connections Per Second |When the number of new connections captured by the listener exceeds the set limit, the excess will be discarded and not forwarded to the backend server. | **✓**  | **✓**  | **✓**  | **✓**  |
|Limits the listener's max connections |When the number of concurrent connections captured by the listener exceeds the upper limit set, the excess will be discarded and will not be forwarded to the backend server. | **✓**  | **✓**  | **✓**  | **✓**  |
|Session persistence |After enabling, when a backend server is deleted or a health check exception occurs, existing connections will transmit normally within the connection draining timeout period. | **✓**  | **✓**  | **×**  | **×**  |
|Gzip data compression |When the client request header carries `accept-encoding: gzip`, if the backend server returns files of specific types (including text/plain, text/css, text/xml, application/xml, text/javascript, application/x\-javascript, application/json, application/javascript, application/x\-protobuf) to the client, the CLB compresses them before returning to the client. | **×**  | **×**  | **✓**  | **✓**  |
