---
title: "What is Vortex IP"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/What_is_Vortex_IP"
---

Vortex IP, a service from BytePlus, is an internet proxy solution for international users. It masks your original IP, enables a higher rate of requests, and provides fast, stable internet access.

<span id="uJvYayv4"></span>
## Service type


|Service type |Description |Application scenario |
|---|---|---|
|Dynamic data center proxy |With the dynamic data center proxy service, Vortex IP provides millions of datacenter egress IP addresses in strategic countries worldwide. Through these IPs, you can quickly and efficiently access global websites. |* Websites that need to be accessed with low\-cost, high\-bandwidth, and low\-latency.<br><br>* Websites with simple access restrictions. |
|Dynamic residential proxy |With the dynamic residential proxy service, Vortex IP provides hundreds of millions of dynamic residential egress IP addresses distributed across more than a hundred countries worldwide. This enables you to access global websites as a real user. |* Websites with complex access restrictions that need to be accessed using a real user identity.<br><br>* Websites requiring an improved access success rate. |
|Video\-specific proxy |With the video\-specific proxy service, Vortex IP provides egress IP addresses specific for accessing video resources. This enables you to access video websites quickly and reliably. |Scenarios for large\-scale, high\-bandwidth access to video websites. |


<span id="uJvYayv4"></span>
## Access mode


|Access mode |Principle |Access protocol |
|---|---|---|
|VPC mode |Each Vortex IP instance is assigned a service domain. After associating the service IP address with a backend VPC and its subnet, you enable dynamic egress IP translation. This forwards requests from your ECS to the target site, enhancing both access performance and reliability.<br><br> |Supports http, https, and socks5 protocols |
|Internet mode<br><br><div data-tips="true" data-tips-type="default">Notes</div><br><br><br><div data-tips="true" data-tips-type="default">The internet access mode is in the beta stage. If you need a trial, please contact your account manager.</div><br> |Users can access Vortex IP service via the Internet domain. You can configure inbound ACL rules to selectively translate the Internet access IP and forward Internet access requests to the target website, ensuring Internet access security and enhancing user experience. ||


<span id="uJvYayv4"></span>
## Related terms


|Concept |Description |
|---|---|
|Service Domain |Used by Vortex IP to receive access requests sent from the internet egress of ECSs or client devices.<br><br>In Internet mode, to ensure your network security, you can [add whitelist entries](https://docs.byteplus.com/en/docs/gavi-sept-test1/Manage_allowlist_entries#.5pON5L2c5q2l6aqk) to configure an inbound source address whitelist. |
|Egress IP address |Vortex IP sends requests through the egress IP to access the target website. |
