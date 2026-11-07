---
title: "Upstream of fixed IP type"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Fixed_IP_type_Upstream"
---

API Gateway supports connecting to fixed IP addresses, allowing fixed IP addresses that can communicate with the gateway network to be encapsulated as an Upstream to serve as the routing backend for the gateway. This article explains how to create an IP type Upstream.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An API Gateway instance has already been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

* The IP address and port for connection have been obtained.


<span id=".5pON5L2c5q2l6aqk"></span>
## Limit


* The fixed IP address and the VPC where the APIG instance resides can communicate with each other.

* Static IP addresses only support the following private network segments: 172.16.0.0/12, 10.0.0.0/8, and 192.168.0.0/16.

* Elastic IP Address is not supported at this time.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to APIG console.

3. After selecting the target instance in **Instance Management**, click **Upstream List**.

3. On the Upstream list page, click **Create Upstream**.

4. On the Create Upstream page, fill in the parameter information as required.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Upstream name |Customize upstream name The Upstream name must be unique within the same instance. |
      

   * **Backend configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Select the backend service type to connect to Upstream. In this scenario, select **Fixed IP**. |
      |Protocol |Select a protocol type. Support **HTTP1.1**, **HTTP2**, and **HTTP2/GRPC**. |
      |TLS settings |Configure TLS.<br><br><br>* **Disable TLS**: The gateway accesses the Backend Upstream using the HTTP protocol.<br><br>* **One\-way TLS**: The gateway accesses the Backend Upstream using the HTTPS protocol, and the corresponding certificate must be selected. |
      |IP |Configure the backend IP address for connecting to Upstream. Click **Add IP** to configure multiple backend IP addresses.<br><br><br>* A maximum of 5 ports can be added for each IP.<br><br>* Supports adding up to 20 IP addresses. |
      |Port |Configure the port number of the backend IP that Upstream connects to. You can configure multiple port numbers. After entering each port number, press the Enter key to confirm. |
      |Load balancing algorithm |Choose a load balancing algorithm.<br><br><br>* **Poll**: (Default) Distributes all requests sequentially to each IP, and is suitable for scenes where Service specifications are the same.<br><br>* **Random**: Requests are randomly allocated to each IP.<br><br>* **Least connections**: Allocate requests to the IP currently processing the fewest requests.<br><br>* **Consistent hashing**: Load balancing is performed based on header/querystring information, ensuring that users with the same information can consistently access the same IP address when the number of backend services remains unchanged. You can click **Enable Overload Protection**, set **Load Threshold**, and enable instance overload protection. After enabling, if an instance's number of active requests exceeds the threshold for the average number of active requests, the instance will not be selected even if the hash value matches the instance. |
      |Service circuit breaking |Configuration: whether to enable circuit breaking.<br><br>Once enabled, the API Gateway can improve the route hit rate by configuring circuit breakers without consuming additional traffic. For details, see [Circuit breaking policies](https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy). |
      |Warm up time |Configuration is supported only when the load balancing algorithm is set to **Round robin** or **Minimum number of connections**.<br><br>Configure the warm\-up time for the backend service. The value must be in integer format, with a range from 1 to 10000 (excluding 10000), and the unit is seconds. |
      

5. Click **Confirm**.


<span id=".5pS-6KGMIEFQSUcg5a6J5YWo57uE"></span>
## Security group configuration

When the resources corresponding to your IP address and the APIG instance are in the same VPC, but the access port is a non\-standard port (for example, 8080), you need to allow inbound traffic from the APIG security group (named `apig-sg-<accountID>`) on the access port in the relevant security group to ensure that the gateway can successfully access the backend resources corresponding to the IP address.

For example, suppose the access port for the resources corresponding to your fixed IP address is 8080. You need to configure the security group associated with the VPC, add an inbound rule, and allow traffic from the APIG security group to port 8080.
