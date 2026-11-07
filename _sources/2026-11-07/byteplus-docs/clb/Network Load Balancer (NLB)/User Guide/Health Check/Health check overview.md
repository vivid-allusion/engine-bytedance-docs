---
title: "Health check overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview"
---

## Introduction​

Health Check: Determines whether backend servers are functioning normally, preventing requests from being forwarded to abnormal servers and ensuring service availability.

Health checks for a **server group** can be configured not only during [creating server group](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group) but also after it has been created.

> Note that:

> Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload. However, to ensure service continuity, it is not recommended to disable health checks, as doing so may cause requests to be forwarded to abnormal backend servers.

## Classification

Classified based on the protocol used by health checks, as shown in the table below:

|Health check protocol |Explanation |Application scenario |
|---|---|---|
|TCP |Send SYN handshake packets to verify the status of the backend server port. |It is used frequently to check services relying on stable connections, such as email servers and file transfer servers. |
|UDP |Send ICMP or UDP probe messages to check whether the backend server is normal. |It is used frequently to check services with high real\-time requirements, such as online games and video conferences. |
|HTTP |Send HEAD or GET requests to simulate browsing behavior and check if the application of the backend server is functioning properly. |It is used frequently to check web applications, such as e\-commerce websites and social media platforms. |

## Status and health check time

* **Status**

   |Status |Explanation |
   |---|---|
   |Available |All backend servers in the server group are normal. |
   |Exception |There are abnormal backend servers within the server group. |
   |Not enabled |Health check is not enabled for the server group. |
   |No server |No backend server is configured in the server group. |

* **Health check time**

   |Parameter |Explanation |Example |
   |---|---|---|
   |Response timeout |Configure the waiting time for the health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* Value range: 1 to 60 seconds. |2 seconds |
   |Detect interval |The time interval for performing health checks.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 1 to 300 seconds. |5 seconds |
   |Healthy threshold |The number of health checks to mark a backend server as normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Normal**, its status changes from **Abnormal** to **Normal**.<br><br>* Value range: 2 to 10 times. |3 times |
   |Unhealthy threshold |The number of health checks to mark a backend server as abnormal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Abnormal**, its status changes from **Normal** to **Abnormal**.<br><br>* Value range: 2 to 10 times. |3 times |

* **Check process**

   Using the example values from the **Health check time** table above, the health check process is illustrated as follows.

   **TCP/UDP protocols**

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04e0efcd0865abd2ac1738ac362619b0.png)

   **HTTP protocol**

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fd34c4d33129a24a219f106015722192.png)

## Mechanism

The selection rules of server group health check protocol are as follows:

* For server groups using UDP as the backend protocol, it is recommended to configure a UDP health check.

* For server groups with TCP backend protocol, HTTP health checks are recommended to obtain the status codes from backend services. In all other cases, TCP health checks should be configured.

The mechanisms of the health check are as follows:

**TCP health check mechanism**

The TCP server group performs health checks on backend servers by sending SYN packets to detect the status of backend servers. The specific mechanism is as follows:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d805e3b54a7a21110fb17adf7f74770e.png)

1. The NLB instance sends a TCP SYN packet to the "private IP address and port" of the backend server based on the health check configuration of the server group.

2. After receiving the request, if the corresponding port on the backend server is listening normally, it will return a SYN+ACK packet.

3. If the NLB instance receives the packet returned by the backend server before the Response timeout period expires, it determines that the service is running normally and the health check is successful. It further sends an ACK packet and then sends an RST packet to the backend server to release the TCP connection.

4. If the NLB instance does not receive the packet from the backend server before the Response timeout period expires, it determines that the service is not responding and the health check fails. Then, the NLB instance sends an RST packet to the backend server to release the TCP connection.

> **tip**

> Normal TCP 3\-way handshake: The NLB instance sends a SYN packet to the backend server\-\-\>The backend server sends a SYN+ACK packet back to the NLB instance\-\-\>The NLB instance sends an ACK packet to the backend server, and a connection is successfully established for data transmission. For TCP health checks, the system sends an ACK packet followed immediately an RST packet to release the TCP connection.

> This implementation mechanism may cause the backend server to consider the related TCP connection to have exited with an exception and throw an error message, such as `Connection reset by peer`. Solution:

* > Apply the HTTP protocol for health checks.

* > After the server group enables the feature to obtain the client source IP, connection errors from the health check can be ignored.

**HTTP health check mechanism**

The HTTP server group performs a health check on the backend server, simulating browser access requests by sending GET/HEAD requests to detect the status of the backend server. The specific mechanism is as follows:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd9b1e409fab26f3653b43b24924641a.png)

1. The NLB instance sends GET/HEAD requests to either the backend server's "private IP + port" or "domain + path + port" configuration, based on the server group's health check settings.

2. The backend server responds with the HTTP status code based on the running status of the corresponding service after receiving the request.

3. If the NLB instance does not receive any information from the backend server within the Response timeout period, which marks the server as abnormal and the health check as a failure.

4. If the NLB instance receives information from the backend server within the Response timeout period, it validates the health check by comparing the returned HTTP status code against the preconfigured expected status code. If the codes match, the health check is successful.

**UDP health check mechanism**

Perform a health check on the server group using the UDP protocol. The implementation mechanism differs slightly depending on whether the health check characters are specified, as shown in the following figure:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65cf797fa00c430f98dbcbbb18ce32d6.png)

* When the health check characters are not specified, the UDP listening check works as follows:

   1. The NLB instance sends an ICMP packet to the private IP address of the backend server.

   2. The NLB instance sends a UDP detection packet to the private IP address and health check port of the backend server.

   3. If within the Response timeout period, the ICMP packet is sent successfully and the NLB instance does not receive an error message such as port unreachable from the backend server, the health check is deemed successful; otherwise, it is deemed a failure.

* When the health check characters are specified, the UDP listening check works as follows:

   1. The NLB instance sends a UDP detection packet to the private IP address and health check port of the backend server based on the specified health check string.

   2. If the NLB instance receives the expected information from the backend server before the Response timeout expires, the health check is successful. Otherwise, the health check fails.

> **tip**

* > UDP listener health check may incorrectly report health status inconsistent with the actual service status.

* > When the backend server operating system is Linux, its ICMP attack protection limits the ICMP sending rate under high concurrency scenarios. Abnormal backend servers cannot return error messages promptly, causing the listener to falsely report health check success.
