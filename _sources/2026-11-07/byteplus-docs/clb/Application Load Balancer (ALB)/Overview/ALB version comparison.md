---
title: "ALB version comparison"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Comparison-between-instance-editions"
---

<span id="2abc8c34"></span>
### Version description

ALB offers two instance editions—Basic Edition and Standard Edition—to meet the load balancing needs of applications at different scales:


|ALB instance edition |Explanation |
|---|---|
|**Basic edition** |* Suitable for small\-scale applications<br><br>* Provides basic Load Balancer capabilities<br><br>* Supports simple forwarding rules based on domain names and paths |
|**Standard edition** |* Suitable for medium to large\-scale applications<br><br>* Supports advanced forwarding features such as HTTP header request forwarding<br><br>* Flexible forwarding rule priority adjustment |


<span id="e2213b7a"></span>
### Version selection advice

Standard Edition and Basic Edition instances follow the same billing standards. It is recommended to use Standard Edition instances to access richer product features and more flexible configuration options.

<span id="9a4458bc"></span>
### Feature Support by Edition

The table below outlines the support status of specific features across the different instance editions.


|**Feature module** |**Feature** |**Basic edition** |**Standard edition** |
|---|---|---|---|
|**Instance** |Multiple availability zones |Support |Support |
||Instance domain name |Support |Support |
||Dual\-stack instance |Supported (requires application) |Supported (requires application) |
||Network type change |Support |Support |
||Instance delete protection and modification protection |Support |Support |
||Availability zone change |Support (requires application) |Support (requires application) |
||WAF protection |Support |Support |
||Access log delivery to TLS |Support |Support |
|**Listener** |HTTP and HTTPS protocols |Support |Support |
||HTTP/2 protocol |Support |Support |
||WebSocket protocol |Support |Support |
||QUIC protocol |**Not support** |Supported (requires application) |
||SNI extension certificate smart optimization |**Not support** |Support |
||Access control |Support |Support |
|**Forwarding rules** |HTTP header\-based forwarding |**Not support** |Support |
||Forwarding rule priority adjustment |**Not support** |Support |
||Compound forwarding conditions ("AND", "OR") |**Not support** |Support |
||Forwarding rules associated with multiple server groups |**Not support** |Support |
||Redirection |Support |Support |
||Rewrite |**Not support** |Support |
||**Cross\-domain** |**Not support** |Supported (requires application) |
|**Server Group** |Cookie\-based session persistence |Support |Support |
||Health check |Support |Support |
||IP\-type server group |Supported (requires application) |Supported (requires application) |
||Communication protocol HTTPS |**Not support** |Supported  |
||Communication protocol gRPC |**Not support** |Supported (requires application) |
|**Custom configuration** |Timeout Configuration |Support |Support |
||TLS protocol version configuration |Support |Support |
||TLS v1.3 version |Support |Support |
||Encryption cipher suite configuration |Support |Support |
||Custom request header |Support |Support |
||Custom response header |Support |Support |


<span id="a68f0411"></span>
### Performance and Capacity Differences

The default performance and capacity are the same for ALB instances of both editions. However, the performance capacity of Standard Edition ALB instances can be adjusted. If your required performance exceeds the default capacity, please Submit ticket or contact your account manager to apply.


|**Performance metric** |**Basic edition** ||**Standard edition** ||
|---|---|---|---|---|
||default |Adjustable |default |Adjustable |
|Queries Per Second (QPS) |100,000 |No |100,000 |Yes |
|Concurrent connections |1,000,000 |No |1,000,000 |Yes |
|New connections per second |100,000 |No |100,000 |Yes |
|Intranet bandwidth |10 Gbps |No |10 Gbps |Yes |
