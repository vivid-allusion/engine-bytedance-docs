---
title: "Adding CLB access configurations"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Adding_CLB_access_configurations"
---

This topic describes how to add a Cloud Load Balancer (CLB) access configuration for microservices applications.

<span id="5z9QlwrJ"></span>
## Background information

If an application is accessible only through its private IP address, an application modification or restart causes a change to the private IP address, which makes the application inaccessible. Associating a CLB instance with the application enables users to access the application by using the fixed public or private IP address of the CLB instance. Additionally, the CLB instance enables load balancing among application instances and thereby effectively improves the overall application performance and stability.

<span id="CAqCk052"></span>
## Limits


* A CLB configuration can be added only to an existing microservices application function. You cannot configure CLB settings when you create a microservices application function.

* The CLB instance and microservices application function must be within the same virtual private cloud (VPC).

* You cannot use a CLB instance that has been used by another service.

* A single CLB supports adding a maximum of 5 listening ports.

* For the CLB listening configurations already set up on the function side, it is recommended to manage them **only on the function side**. Do not modify the configurations on the CLB side to avoid conflicts.


<span id="inHlFrgQ"></span>
## Prerequisites


* A microservices application has been created and released. For details, see [Creating microservices applications](https://docs.byteplus.com/en/docs/faas/Create_microservices_applications).

* A CLB instance has been created in the same VPC as the microservices application. For details, see  [Creating CLB instances](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).

* The security group configuration has been completed. For the inbound direction of the security group, allow traffic where the source address is 100.64.0.0/10, and the request protocol and destination port match the backend server port. For details, see [Configure Backend Server Security Group.](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group)

* (Optional) When configuring a public network CLB, it is necessary to allow inbound public network access to the container\-side ports (excluding CLB virtual IP ports) in the container security group. By default, only ports 80 and 443 are open, and other ports need to be configured manually.


<span id="foXDT2Dd"></span>
## Procedure


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Function**.

4. In the function list, click the name of the function of the microservices application.

5. Click **Function configuration** \> **App access settings**. Click the edit icon next to **Private network CLB access address** or **public network CLB access address** to add a CLB access configuration.

   
   |Parameter |Description |
   |---|---|
   |CLB instance |Select an existing CLB instance. |
   |scheduling strategy |Select the scheduling strategy for load balancing.<br><br><br>* **Weighted polling (WRR)** : Distributes requests cyclically according to preset instance weights. Higher\-weight instances receive more traffic. This strategy features simple logic and easy implementation and is applicable to scenarios with evenly distributed requests and tiered instance performance.<br><br>* **Weighted minimum number of connections (WLC)** : Routes requests to instances with the lowest ‌weight\-adjusted active connections‌ (combining instance weights and real\-time connection counts). This strategy is applicable to environments with volatile request loads.<br><br>* **Source address hash (sh)** : Hashes the source IP address of requests to consistently route traffic to the same instance. This strategy ensures ‌session persistence‌ and is ideal for services that rely on local session state. |
   |Select listening port |Select the listening protocol.<br><br><br>* **TCP protocol**: A connection\-oriented transport layer protocol that supports retransmission, flow control, and congestion control, ensuring reliable and ordered data transmission. It is applicable to scenarios with high reliability requirements.<br><br>* **UDP protocol**: A connectionless transport layer protocol that does not require establishing a connection. It enables fast transmission speed without guaranteed data reliability or order, has low overhead, and is applicable to scenarios with high real\-time requirements, such as video calls. |
   |TCP protocol |This parameter is available if you select **TCP protocol** for **Select listening port**. Enter the port numbers for the CLB side and the Vital Kubernetes Engine (VKE) side. You can add multiple ports. |
   |UDP protocol |This parameter is available if you select **UDP protocol** for **Select listening port**. Enter the port numbers for the CLB side and the Vital Kubernetes Engine (VKE) side. You can add multiple ports. |
   

6. Click **Add**.



&nbsp;

&nbsp;


&nbsp;

&nbsp;

&nbsp;

&nbsp;
