---
title: "Forward DNS queries from the on-premise IDC/third-party cloud services to the resolver"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/forward_dns_from_idc"
---

If you need to forward DNS requests from the on\-premise IDC/third\-party cloud services to the resolver, you need to create an inbound VPC, inbound endpoint, and rules in BytePlus PrivateZone.


* **Inbound VPC**: Used to establish network connections with on\-premise IDC/third\-party cloud service. You can create a new VPC as the inbound VPC or use an existing VPC as the inbound VPC. You need to establish network connections using Direct Connect or VPN.

* **Inbound endpoint**: Located in the inbound VPC, it serves as the entry point for DNS queries. After receiving DNS queries from external sources, the inbound endpoint forwards these requests to the resolver. To ensure high availability, an inbound endpoint requires at least one IP address in each subnet corresponding to two different availability zones.

* **Rule**: Created by you in the DNS server of your on\-premise IDC/third\-party cloud service. It specifies information such as the domain names for which DNS queries need to be forwarded, the IP addresses of the DNS servers corresponding to the inbound endpoints, and other relevant details.


<span id="how-the-inbound-endpoint-forwards-dns-queries-to-the-resolver"></span>
### How the inbound endpoint forwards DNS queries to the resolver


1. When a user of the on\-premise IDC/third\-party cloud services accesses `a.example.com`, they send a DNS query to the DNS server in the on\-premise IDC/third\-party cloud services. The DNS server forwards the DNS query to the inbound endpoint according to the rules.

2. The inbound endpoint forwards the DNS query to the resolver.

3. The resolver returns the IP address to the inbound endpoint.

4. The inbound endpoint returns the IP address to the DNS server of the on\-premise IDC/third\-party cloud services. The DNS server returns the IP address to the user.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2bee737b380851b36e73a9b0d20de4a1.jpg) </span>

<span id="steps"></span>
### Steps

Refer to the following steps to forward DNS queries from external sources to the resolver.


1. [Develop an inbound DNS strategy](https://docs.byteplus.com/docs/byteplus-dns-suite/NjbB4q)

2. [Create an inbound VPC](https://docs.byteplus.com/en/docs/6758/1169910)

3. [Create inbound endpoints](https://docs.byteplus.com/en/docs/6758/1169911)

4. [Create rules in the DNS server of the on-premise IDC/third-party cloud services](https://docs.byteplus.com/en/docs/6758/1171695)

5. [Verify DNS response](https://docs.byteplus.com/en/docs/6758/975683)
