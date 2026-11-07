---
title: "Resolve DNS Queries Between VPC and On-premise IDCs/Third-party Cloud Services"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/OoOiVP"
---

In a hybrid cloud scenario, your BytePlus cloud resources and on\-premise IDC/third\-party cloud services are generally connected through dedicated lines, VPNs, cloud enterprise networks, or transit routers. If your service needs to use both BytePlus virtual private network (VPC) and resources in a on\-premise IDC/third\-party cloud services, your service may need to meet the following DNS resolution requirements:

* VPC users access resources in on\-premise IDC/third\-party cloud services through domain names.

* Users of on\-premise IDC/third\-party cloud services access resources in the VPC through domain names.

To meet these requirements, DNS queries need to be forwarded from the VPC to the on\-premise IDC/third\-party cloud services, or from the on\-premise IDC/third\-party cloud services to the VPC. BytePlus PrivateZone can forward DNS queries through resolvers, outbound endpoints, inbound endpoints, and rules:

* **Outbound endpoint**: forwards DNS queries from the VPC to the DNS server in your on\-premise IDC/third\-party cloud services.

* **Inbound endpoint**: forwards DNS queries from the on\-premise IDC/third\-party cloud services to the resolver.

* **Rule**: specifies the domain names and target IP addresses for forwarding DNS requests.

Using resolvers to forward DNS queries incurs fees. See [Billing](https://docs.byteplus.com/docs/byteplus-dns-suite/43T5hU).
