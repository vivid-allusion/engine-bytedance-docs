---
title: "Load Balancer overview"
product: "Cloud Load Balancer"
product_code: "clb"
section: "Document"
source: "https://docs.byteplus.com/en/docs/clb/Load-Balancer-overview"
---

<span id="URWBqzOy"></span>
## Overview

Load Balancer is a service that distributes client access requests to a group of backend servers according to predefined scheduling algorithms. It effectively balances server loads and prevents service unavailability caused by single\-server overload or failure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56a801b47721e252e548649f80ace249.png) </span>

<span id="wbYDqOBu"></span>
## Classification


|Classification |Notes |Application scenario |Documentation |
|---|---|---|---|
|Network Load Balancer (NLB) |NLB specializes in Layer\-4 load balancing scenarios, supporting TCP, UDP, and TLS protocols **.**  It delivers highly elastic and low\-latency traffic forwarding capabilities. |Suited for high\-throughput, low\-latency scenarios |[What is Network Load Balancer](https://docs.byteplus.com/en/docs/clb/What-is-Network-Load-Balancer) |
|ALB |ALB provides Layer 7 load balancing services, supporting HTTP, HTTPS, HTTP/2, and QUIC protocols. It delivers robust processing capabilities such as TLS/SSL offloading. ALB enables advanced content\-based routing—including domain name, URL path, HTTP headers, and request methods—to perform request forwarding, redirection, and rewriting. It is deeply integrated with Vital Kubernetes Engine (VKE) and can serve as a cloud\-native Ingress. |Suitable for scenarios requiring complex business logic processing and fine\-grained traffic routing<br><br> |[What is an Application Load Balancer](https://docs.byteplus.com/en/docs/clb/Introduction) |
|CLB |The CLB delivers robust Layer 4 capabilities and fundamental Layer 7 capabilities. By listening on TCP, UDP, HTTP, and HTTPS, it offers both stable, high\-efficiency forwarding for transport layer services and meets basic intelligent management needs for application layer traffic. |Designed for scenarios requiring both Layer 4 capabilities and basic Layer 7 capabilities. |[What is a Classic Load Balancer](https://docs.byteplus.com/en/docs/clb/Product-Overview-01)<br><br> |


<span id="Bm42uest"></span>
## Features


|Comparison item |ALB |NLB |CLB |
|---|---|---|---|
|Product positioning |Based on protocols such as HTTP, HTTPS, HTTP/2, WebSocket, and QUIC, it provides Layer\-7 load balancing capabilities. |By leveraging TCP, UDP, and TLS protocols, it provides robust Layer\-4 load balancing capacity.<br><br> |Operates based on TCP, UDP, HTTP, and HTTPS protocols, providing comprehensive Layer 4 and Layer 7 load balancing capabilities. |
|Network performance |A single instance supports up to 1 million QPS.<br><br> |Adaptive instance performance. A single instance supports up to 100 million concurrent connections and 100 Gbps bandwidth. |Instance performance is constrained by its specifications. A single instance supports up to 1 million concurrent connections and 10 Gbps bandwidth. |
|Traffic forwarding |* Support content\-based request routing—including domain name, URL path, HTTP headers, and request methods—to perform request forwarding, redirection, and rewriting.<br><br>* ​Support for adjusting the priority of forwarding rules​​.<br><br><br> |Supports Layer\-4 traffic forwarding based on IP/port, including full\-port listening and session persistence.<br><br> |Layer\-7 rules are simple (e.g., basic path forwarding), while Layer\-4 functionality remains the primary focus. |
|Disaster recovery capability |Active\-active disaster recovery across Availability Zones |Active\-active disaster recovery across Availability Zones |Active and standby availability zones for disaster recovery |
|Access control |Access control is implemented through allowlist/denylist policy groups.<br><br> |Reuse the security group and Network Access Control List to implement Identity and Access Management (IAM) |Access control is implemented through allowlist/denylist policy groups.<br><br> |
|Health Check |Supports health checks based on both TCP and HTTP protocols |Supports on\-demand selection of health check protocols and ports<br><br> |Supports Layer 4 (TCP) and basic Layer 7 (HTTP status code) health checks |
|Backend Mounting Capability |* Server groups operate independently from the instance, and a single server group can be mounted to multiple different instances. Multiple server groups can be added under a single forwarding rule​​.<br><br>* Backend Communication Protocol:​​ Communication with backend servers can use HTTP, HTTPS, or gRPC.<br><br>* Supported Backend Types:​​ Backend servers can be ECS instances, secondary ENIs attached to ECS instances, IP addresses, or Elastic Container Instances.<br><br>* Communication IP Range:​​ The instance uses IP addresses from the 100.64.0.0/10 segment to communicate with the backend servers. When backend servers are IP addresses from a different VPC or an on\-premises IDC, after establishing connectivity via Cloud Enterprise Network (CEN) or a Transit Router, you must additionally configure the return route, which increases the configuration complexity. |* Server groups operate independently from the instance, and a single server group can be mounted to multiple different instances.<br><br>* For IP\-mode backend server groups, the communication between the instance and the backend server uses the IP address within the instance's VPC. When connected via Cloud Enterprise Network (CEN) or Transit Routers, routes propagate automatically, requiring no manual routing configuration.<br><br><br> |* The server group belongs to the instance and can only be mounted to its associated instance.<br><br>* For IP\-mode server groups, communication with backend servers uses IP addresses from 100.64.0.0/10 range. When connecting through Cloud Enterprise Network (CEN) or Transit Router (TR). Manual return\-path routing configuration is required, introducing considerable configuration complexity. |
|Logs management |Support access log and health check log |Support access log |Support access log and health check log |
|Data monitoring |Provides data monitoring capabilities at both the instance and listener dimensions<br><br> |Offers instance\- and listener\-level data monitoring and pre\-configured alert templates |Offers instance\- and listener\-level data monitoring and pre\-configured alert templates |


&nbsp;

<span id="g5tIjGtg"></span>
## Billing

The sub\-products under the Load Balancer category support different billing methods, and the billable items involved also vary by method. You can refer to the following billing instructions for details on the billing methods and billable items of each sub\-product.


<Tabs>
<Tab zoneid="E5ueXs0LJN" title="ALB billing note">
<TabTitle>ALB billing note</TabTitle>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_341a027c29ca31f85046cb59507deb4c.png) </span>


* Pay\-by\-CU: For details, see [Pay-by-CU](https://docs.byteplus.com/en/docs/clb/Billing-rules).

* ALB resource package: For details, see [ALB resource package](https://docs.byteplus.com/en/docs/clb/Resource-packages).


</Tab>
<Tab zoneid="eWffKvRekH" title="NLB billing note">
<TabTitle>NLB billing note</TabTitle>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8aced6871224beb66b0b79e74fb6886.png) </span>


* Pay\-by\-CU: For details, see [Pay-by-CU](https://docs.byteplus.com/en/docs/clb/NLB-Pay-by-LCU).

* NLB Resource Package: For details, see [NLB Resource Package](https://docs.byteplus.com/en/docs/clb/NLBPackages).


</Tab>
<Tab zoneid="H3MgansAA7" title="CLB billing note">
<TabTitle>CLB billing note</TabTitle>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b8a04056edf69ac8a5210ab55a246c0.png) </span>


* Pay\-as\-you\-go: see [Pay-as-you-go](https://docs.byteplus.com/en/docs/clb/Billing-02) for details.

* Subscription: see [Subscription](https://docs.byteplus.com/en/docs/clb/Billing-04) for details.


</Tab>
</Tabs>


<span id="LJ6NNwg5"></span>
### LCU billing


|Product type |LCU calculation rules |Reference documentation |
|---|---|---|
|NLB<br><br> |* When converting resource usage for TCP listeners to LCUs, the conversion relationship is as follows:<br><br>   * New connections per second: 800 / LCU<br><br>   * Concurrent connections per minute: 100,000 / LCU<br><br>   * Data processed: 1 GB / LCU<br><br>* When converting resource usage for UDP listeners to LCUs, the conversion relationship is as follows:<br><br>   * New connections per second: 400 / LCU<br><br>   * Concurrent connections per minute: 50,000 / LCU<br><br>   * Data processed: 1 GB / LCU<br><br>* When converting resource usage for TLS listeners to LCUs, the conversion relationship is as follows:<br><br>   * New connections per second: 50 / LCU<br><br>   * Concurrent connections per minute: 3,000 / LCU<br><br>   * Data processed: 1 GB / LCU |[Pay-by-CU](https://docs.byteplus.com/en/docs/clb/NLB-Pay-by-LCU)<br><br> |
|ALB |When converting resource usage to LCUs, the conversion relationship is as follows:<br><br><br>* New connections per second: 25 / LCU<br><br>* Concurrent connections per minute: 3,000 / LCU<br><br>* Data processed: 1 GB / LCU<br><br>* Rule evaluations: 1,000 / LCU<br><br><br>> Rule evaluations are calculated based on the number of forwarding rules and QPS. Each instance includes a free quota of 30 forwarding rules. |[Pay-by-CU](https://docs.byteplus.com/en/docs/clb/Billing-rules) |


<span id="sYh25CyO"></span>
### Resource Package


|Product type |Billing rules |Reference documentation |
|---|---|---|
|NLB |NLB Resource Package is a pre\-purchased bundle of LCUs designed to offset the LCU fees and instance fees for NLB instances billed on a usage basis.<br><br><br>* Instance Fee: The offset ratio is 4:1, meaning 1 LCU covers the instance fee for one NLB instance for one hour.<br><br>* LCU Fee: The offset ratio is 1:1, meaning one LCU offsets the actual consumption of one LCU by an NLB instance. |[NLB resource pack](https://docs.byteplus.com/en/docs/clb/NLBPackages) |
|ALB |ALB Resource Package is a pre\-purchased bundle of LCUs designed to offset the LCU fees and instance fees for ALB instances billed on a usage basis.<br><br><br>* Instance Fee: The offset ratio is 1:1, meaning 1 LCU covers the instance fee for one ALB instance for one hour.<br><br>* LCU Fee: The offset ratio is 1:1, meaning one LCU offsets the actual consumption of one LCU by an ALB instance. |[ALB resource package](https://docs.byteplus.com/en/docs/clb/Resource-packages)<br><br> |
