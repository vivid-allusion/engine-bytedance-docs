---
title: "Limits"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Limits"
---

This topic describes the default quotas for PrivateLink\-related resources within a single account and region.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The default throughput for an endpoint connection is 10 Gbps. If this does not meet your needs, see [Adjusting an endpoint connection rate limiting](https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting#.6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf).

* A single Interface Endpoint supports associating with a maximum of 5 security groups.

* Each endpoint supports one elastic network interface (ENI) per Availability Zone.

* An interface endpoint and its associated endpoint service support the TCP and UDP protocols.

* A single VPC can have a maximum of one gateway endpoint.

* Each endpoint service supports configuring only one private DNS name (i.e., custom domain name).

* A single ALB instance can be added to endpoint services a total of 200 times (this count is calculated per Availability Zone).

   For example, consider an ALB instance is deployed across Availability Zone A, B, and C. When this ALB is added to the endpoint service with both Availability Zone A and B selected, it consumes 2 additions from the quota. The remaining times this ALB instance can be added to the endpoint service is: 200\-2=198 times.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The ALB service resource support for PrivateLink is in beta stage. For trial requests, contact your account manager.   </div>
   

<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limits

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the adjustable quota items listed in the table below, if the default quantity is insufficient, you can go to the <a href="https://console.byteplus.com/quota/productList">Quota Center</a> to request an increase for the corresponding quota.</div>



|Network resources |Quota parameter |Description |Maximum |Support adjustment |Adjustable limit |
|---|---|---|---|---|---|
|&nbsp;<br><br>Endpoint Service |endpoint_service |Maximum number of Endpoint Services a single account can create |100 |&nbsp;<br><br>Yes<br><br> |200 |
||endpoint_service/zone/resource |Number of service resources that can be added per Availability Zone for a single endpoint service |100 ||200 |
|&nbsp;<br><br>End point node |endpoint |Maximum number of interface endpoints creatable per account |500 |&nbsp;<br><br>Yes<br><br> |800 |
||vpc/endpoint |Number of interface endpoints that can be created in a single VPC |50 ||80 |
|&nbsp;<br><br>Zone |endpoint_service/zone |Number of Availability Zones to which service resources can be added for a single endpoint service |Number of Availability Zones supported in a region |&nbsp;<br><br>No<br><br> |&nbsp;<br><br>\-\- |
||endpoint/zone |Maximum number of Availability Zones a single endpoint can be created in |Number of Availability Zones supported in a region |||
