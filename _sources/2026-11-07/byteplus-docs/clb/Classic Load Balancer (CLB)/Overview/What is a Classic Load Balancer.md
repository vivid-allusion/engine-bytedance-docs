---
title: "What is a Classic Load Balancer"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Product-Overview-01"
---

The Classic Load Balancer (CLB) service distributes access traffic to multiple servers based on set policies. This service expands the external service capabilities of your system and eliminates single points of failure, improving the overall availability of the system.

<span id=".5Lqn5ZOB5p625p6E"></span>
## Product architecture

After a CLB instance provides external services, once the listener captures access requests on specified protocols and ports, the CLB forwards these requests to healthy backend servers within the Server Group attached to the listener according to its configured scheduling algorithm. The product architecture is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_933f809cace02437abe16bf74c62120b.png) </span>


|Components |Explaination |
|---|---|
|Internet |Users can access CLB services through an EIP. |
|CLB instance |The CLB instance receives user access requests and forwards them to the backend servers based on the configuration of the listener and the Server Group.<br><br>When the Region supports active and standby Availability Zones, the CLB instance is deployed in two Availability Zones.<br><br><br>* In normal cases, the active availability zone is enabled, and the standby availability zone does not carry traffic.<br><br>* When the active Availability Zone fails, the system automatically switches to the standby Availability Zone to continue providing CLB. |
|Listener |The listener is responsible for monitoring incoming user access requests to the CLB instance based on the specified protocol and port.<br><br><br>* Protocol: TCP, UDP, HTTP, HTTPS<br><br>* Port: 1 to 65535.<br><br><br>You also need to configure the scheduling algorithm and health check for the listener.<br><br><br>* **Scheduling algorithm**: Used to distribute access requests reasonably to the backend server, avoiding scenarios where one server is overloaded while others remain idle.<br><br>* **Health check**: Used to determine whether the backend server status is normal, preventing requests from being forwarded to backend servers with abnormal status, thus ensuring service availability.<br><br><br>A Layer\-4 (TCP, UDP) listener can only attach one Server Group, while a Layer\-7 (HTTP/HTTPS) listener can specify multiple Server Groups through forwarding rules.<br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/Listeners-01) |
|Backend Server Group |Server group is a group of backend servers.<br><br><br>* Add backend servers, supported formats are as follows:<br><br>   * Elastic Compute Service (ECS): ECS in the same Virtual Private Cloud (VPC) as the CLB instance or secondary network interfaces already mounted on ECS.<br><br>   * IP address: Only IPv4 addresses are supported, as long as the network is reachable.<br><br>* A Server Group can be associated with multiple listeners.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/Server-Group-Overview) |


<span id="FclAQkQa"></span>
## Classification

To help users understand, we have classified CLB:


|Classification |Explaination |Applicable scenarios |
|---|---|---|
|Public CLB |The EIP is created together with the CLB instance, and its **lifecycle** is associated with the CLB instance. When the CLB is released, the Elastic IP is also released along with it. |CLB instances are managed together with EIP. |
|Private CLB |CLB instances without an EIP, or cases where the lifecycle of the EIP and the CLB instance are independent. |Scenario where CLB instances and Elastic IPs are managed separately. |
|Entrusted CLB |CLB instances created by cloud services. The CLB console only supports view functionality and does not allow modifications. |CLB is used by other cloud\-managed services, such as Vital Kubernetes Engine. |


<span id="HTSKzuUm"></span>
## Related products


|Product |Feature Description |
|---|---|
|[Elastic Compute Service (ECS)](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service) |ECS instances serve as the backend servers of a CLB instance and receive traffic. |
|[Virtual Private Cloud (VPC)](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) |Provides a private network deployment environment for a CLB instance. |
|[Elastic IP (EIP)](https://docs.byteplus.com/en/docs/eip/What-is-EIP) |Enables a CLB instance to connect to the IPv4 network (Internet). |
|[IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway) |Enables a CLB instance to connect to the IPv6 internet.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">IPv6 gateway is in the beta stage, please contact your account manager.</div><br> |
