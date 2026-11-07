---
title: "Step 1: Develop an Inbound DNS Strategy"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/NjbB4q"
---

This document describes how to develop inbound DNS policies based on your needs.

<span id="scenario-examples"></span>
## Scenario examples

In the following example scenarios, you can develop corresponding inbound DNS policies.

<span id="multi-cloud-hybrid-cloud-scenario"></span>
### Multi\-cloud/Hybrid cloud scenario

In a multi\-cloud/hybrid cloud scenario, the resolver receives DNS queries from on\-premise IDC/third\-party cloud services through inbound endpoints and returns DNS results.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bb8cefcf1584b153b634242d0caf84df.jpeg) </span>

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">In the following scenarios, the IP address of the external DNS system in the forwarding rules associated with the outbound endpoint cannot be the same as the IP address of the inbound endpoint.</div>



* <div data-tips="true" data-tips-type="danger">The inbound VPC and outbound VPC are connected via Direct Connect or VPN.</div>


* <div data-tips="true" data-tips-type="danger">The outbound VPC and inbound VPC are the same.</div>



<span id="resolving-the-issue-of-dns-failure-after-enabling-cloud-firewall"></span>
### Resolving the issue of DNS failure after enabling cloud firewall

In a multi\-cloud/hybrid cloud scenario, you configure [BytePlus Cloud Firewall](https://www.volcengine.com/docs/6516/76355) for your VPC on the Volcano Engine side to intercept, filter, and monitor all incoming traffic from on\-premise IDC/third\-party cloud services. Traffic from on\-premise IDC/third\-party cloud services will first pass through the cloud firewall VPC, be processed by the cloud firewall, and then forwarded to your VPC.

Suppose the DNS server of the on\-premise IDC/third\-party cloud service needs to access the BytePlus PrivateZone resolver through the IP address `100.96.0.2`. Due to the default route of `100.64.0.0/10` in the cloud firewall's VPC, DNS queries will be directly routed from the cloud firewall's VPC to the BytePlus PrivateZone resolver. However, the cloud firewall VPC does not belong to the effective scope of any domain in the BytePlus PrivateZone, resulting in DNS resolution failure.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8d30f46a727b173a42282a6ab1819e3f.jpeg) </span>

To ensure that BytePlus PrivateZone can respond to DNS queries passing through the cloud firewall, you can create an inbound VPC and inbound endpoint to forward DNS queries to the resolver.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_764fcd7050a704cd46e757fc82f7d28e.jpeg) </span>
