---
title: "Fixed domain name type: upstream"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Fixed_domain_name_type_Upstream"
---

API Gateway supports connecting to fixed domain names. Fixed domain names that can communicate with the gateway network can be encapsulated as an Upstream, serving as the gateway's routing backend. This article explains how to create a domain name\-type Upstream.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>[Beta · Apply for trial]</strong>: This feature is currently in the <strong>Beta</strong> phase. To use it, please contact your account manager.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The API Gateway instance has already been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

* The domain name and port to connect to have been obtained.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to APIG console.

3. After selecting the target instance in **Instance Management**, click **Upstream list**.

3. On the Upstream list page, click **Create Upstream**.

4. On the Upstream creation page, fill in the parameter information as required.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Instance |Upstream is an instance\-level resource. Please select the APIG instance to which the current Upstream belongs. |
      |Upstream name |Customize upstream name. The Upstream Name is unique within the same Instance. |
      |Description |Enter remarks for the current Upstream; this field can be left empty. |
      

   * **Backend configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Select the type of backend service that Upstream connects to. In this scenario, choose **fixed domain name**. |
      |Protocol |Select protocol type. Support **HTTP1.1**, **HTTP2**, and **HTTP2/GRPC**. |
      |TLS settings |Configure TLS.<br><br><br>* **Disable TLS**: The gateway accesses the Backend Upstream using the HTTP protocol.<br><br>* **Unidirectional TLS**: The gateway accesses the Backend Upstream using the HTTPS protocol and needs to select the corresponding certificate. |
      |Domain name |Configure the backend domain name for connecting to Upstream. |
      |Port |Configure the port number of the backend domain name that Upstream connects to. You can configure multiple port numbers. After entering each port number, press the Enter key to confirm. |
      |Load balancing algorithm |Choose a load balancing algorithm.<br><br><br>* **Poll**: (Default) All requests are distributed sequentially to each domain name, making it suitable for scenarios with identical service specifications.<br><br>* **Random**: Requests are randomly allocated to each domain name.<br><br>* **Minimum number of connections**: Allocate requests to the domain name currently processing the fewest requests.<br><br>* **Consistent hashing**: Load balancing based on header/querystring information ensures that, when the number of backend services remains unchanged, users with the same information can always access the same domain name. You can click **Enable Overload Protection**, set the **Load Threshold**, and enable instance overload protection. Once enabled, if an instance's active request count exceeds the threshold set according to the average active request count, the instance will not be selected even if the hash value matches the instance. |
      |Service circuit breaking |Configuration: whether to enable circuit breaking.<br><br>Once enabled, the API Gateway can improve the routing hit rate by configuring the circuit breaker without consuming additional traffic. For details, see [Circuit breaking policies](https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy). |
      |Warm up time |Configuration is supported when the load balancing algorithm is set to **Round Robin** or **Least Connections**.<br><br>Configure the backend service warm\-up time. The value must be an integer between 1 and 9999. The unit is seconds. |
      

5. Click **Confirm**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Security group configuration

If the IP address resolved from the fixed domain name is a private IP address, your service is connected via the private IP address. Please configure the security group by following the steps below.


1. Log in to [VPC console](https://console.byteplus.com/vpc/securityGroup).

2. In the top navigation bar, select the project and region of the target resource.

3. In the left navigation bar, click Security Group.

4. Click **Create security group**, select the target VPC, add an inbound rule to the access rules, and then click **Confirm**.
