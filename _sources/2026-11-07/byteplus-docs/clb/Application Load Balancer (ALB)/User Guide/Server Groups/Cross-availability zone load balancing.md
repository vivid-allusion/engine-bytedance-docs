---
title: "Cross-availability zone load balancing"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Cross-zone-load-balancing"
---

<span id="932f21f2"></span>
## Feature description

ALB provides the "cross\-availability zone load balancing" feature. This feature is implemented at two levels:


* ALB instance level: The instance\-level "cross\-availability zone load balancing" feature is enabled by default and cannot be disabled.

* Server group level: The server group\-level "cross\-availability zone load balancing" feature is enabled by default. You can enable or disable this feature for server groups as needed. When you disable this feature for a server group, ALB distributes requests according to the server group’s configuration.


When the ALB instance is deployed across multiple availability zones in one region, there is an instance node in each availability zone. By default, an instance node in one availability zone distributes received requests to backend servers across all availability zones where the instance is located. This method avoids performance bottlenecks caused by insufficient resources in a single availability zone but introduces some access latency.

In scenarios highly sensitive to latency, such as financial transactions, real\-time communication, and the Internet of Things, you can disable the "cross\-zone load balancing" feature at the server group level. After disabling this feature, each instance node distributes incoming requests only to backend servers within the same availability zone, improving business access speed.

<span id="1c09d56b"></span>
## Request routing

The diagram below shows how instance nodes route client requests when the "cross\-zone load balancing" feature is enabled or disabled.

Assume the ALB instance is deployed in availability zone A and availability zone B within a region and has backend servers attached in both zones.

<span id="eb3a4760"></span>
### **Enable the "cross\-zone load balancing" feature**


* Scenario 1: backend servers in availability zone A and availability zone B both have normal health check status

   The instance node in availability zone A receives client requests and distributes them to backend servers in both availability zone A and availability zone B.

   The instance node in availability zone B receives client requests and distributes them to backend servers in both availability zone A and availability zone B.

* Scenario 2: Backend servers in availability zone A have a normal health check status, while backend servers in availability zone B have an exception health check status

   Instance nodes in availability zone A receive client requests and then only distribute them to backend servers in availability zone A.

   Instance nodes in availability zone B receive client requests and then only distribute them to backend servers in availability zone A.

* Scenario 3: Backend servers in availability zone A have a normal health check status, and backend servers in availability zone B are removed from the server group

   Instance nodes in availability zone A receive client requests and then only distribute them to backend servers in availability zone A.

   Instance nodes in availability zone B receive client requests and then only distribute them to backend servers in availability zone A.


<span id="f6665d7c"></span>
### **Disable the “cross\-zone load balancing” feature**


* Scenario 1: Backend servers in both availability zone A and availability zone B have a normal health check status

   Instance nodes in availability zone A receive client requests and then only distribute them to backend servers in availability zone A.

   Instance nodes in availability zone B receive client requests and then only distribute them to backend servers in availability zone B.

* Scenario 2: The health check status of backend servers in availability zone A is normal, while the health check status of backend servers in availability zone B is abnormal

   Instance nodes in availability zone A receive client requests and then distribute the requests only to backend servers in availability zone A

   Instance nodes in availability zone B receive client requests and directly return status code 502

* Scenario 3: The health check status of backend servers in availability zone A is normal, while backend servers in availability zone B are removed from the server group

   Instance nodes in availability zone A receive client requests and then distribute the requests only to backend servers in availability zone A

   Instance nodes in availability zone B receive client requests and directly return status code 503


<span id="bba90f67"></span>
## Limits

When using the cross\-zone load balancing feature, pay attention to the following limits:


* After you disable the cross\-zone load balancing feature of a server group, you cannot enable the cookie\-based session persistence feature Conversely, after you enable the cookie\-based session persistence feature of a server group, you cannot disable the cross\-zone load balancing feature

* For server groups with the “Remote IP” IP type enabled, you cannot disable the “cross\-zone load balancing” feature.

* If you disable the “cross\-zone load balancing” feature for a server group, that server group cannot be associated with a Basic edition ALB instance. For server groups already associated with a Basic edition ALB instance, you cannot disable the server group’s “cross\-zone load balancing” feature.


<span id="a7ae72de"></span>
## Configuration steps

You can enable or disable the server group’s “cross\-zone load balancing” feature in either of the following ways:


* Method 1: Configure this feature during server group creation

   1. On the **server group** page, click **Create server group**.

   2. On the **Create server group** page, set **cross\-zone load balancing**.

* Method 2: Configure this feature by editing after creating the server group

   1. On the **server group** page, find the server group you want to configure, then click its name to open the details page.

   2. Click **Edit** in the upper right corner of the page.

   3. Set **cross\-zone load balancing**.
