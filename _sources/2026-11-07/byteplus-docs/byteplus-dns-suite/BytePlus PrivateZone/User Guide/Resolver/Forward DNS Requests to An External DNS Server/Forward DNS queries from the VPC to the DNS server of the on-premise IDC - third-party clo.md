---
title: "Forward DNS queries from the VPC to the DNS server of the on-premise IDC/third-party cloud services"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/forward_dns_requests_from_the_vpc"
---

If you need to forward DNS requests from the VPC to an external DNS server, you need to create an outbound VPC, outbound endpoint, and rules in BytePlus PrivateZone.


* **Outbound VPC**: Used to establish network connections with on\-premise IDC/third\-party cloud services. You can create a new VPC as the outbound VPC or use an existing VPC as the outbound VPC. You need to establish network connections using Direct Connect or VPN.

* **Outbound endpoint**: Located in the outbound VPC, it serves as the forwarding exit for DNS queries. After receiving DNS queries forwarded by the resolver, the outbound endpoint forwards these requests to external DNS servers. To ensure high availability, an outbound endpoint requires at least one IP address in each subnet corresponding to two different availability zones.

* **Rule**: Created in the resolver. A rule specifies:

   * Domain: The domain name for which DNS queries need to be forwarded.

   * Scope: One or more VPCs where the rule takes effect. The scope of a rule can include the outbound VPC.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The VPCs within the scope of the rule must be in the same region as the outbound VPC. The resolver cannot forward DNS queries to VPCs in other regions.      </div>
      

   * Outbound Endpoint: The outbound endpoint associated with the rule.

   * Forwarding target address: The IP address of the external DNS server.


<span id="how-the-resolver-forwards-dns-queries-to-the-dns-server-of-the-on-premise-idc-third-party-cloud-services"></span>
### How the resolver forwards DNS queries to the DNS server of the on\-premise IDC/third\-party cloud services


1. When a user in the VPC accesses `a.example.com`, they send a DNS query to the resolver.

2. The resolver forwards the DNS query for `a.example.com` to the outbound endpoint according to the rules.

3. The outbound endpoint forwards the DNS query to the DNS server of the on\-premise IDC/third\-party cloud services.

4. The DNS server returns the IP address corresponding to `a.example.com` to the outbound endpoint.

5. The outbound endpoint returns the IP address to the resolver.

6. The resolver returns the IP address to the user in the VPC.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_737fc8549e7361f73b1cd21f264dd410.jpeg) </span>

<span id="steps"></span>
### Steps

Refer to the following steps to forward DNS queries from the VPC to an external DNS server.


1. [Develop an outbound DNS strategy](https://docs.byteplus.com/docs/byteplus-dns-suite/AETHPc)

2. [Create an outbound VPC](https://docs.byteplus.com/docs/byteplus-dns-suite/XR2p4Q)

3. [Create outbound endpoints](https://docs.byteplus.com/docs/byteplus-dns-suite/OxDblm)

4. [Create a rule in the resolver](https://docs.byteplus.com/docs/byteplus-dns-suite/Zd7JQO)

5. [Verify DNS response](https://docs.byteplus.com/docs/byteplus-dns-suite/IdrNXF)
