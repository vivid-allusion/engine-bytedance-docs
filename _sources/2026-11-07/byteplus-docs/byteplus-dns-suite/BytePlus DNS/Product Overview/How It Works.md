---
title: "How It Works"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-how-it-works"
---

This document introduces how BytePlus DNS works.

<span id="bde7e310"></span>
## How does BytePlus DNS resolve a domain name?

The DNS resolution process starts from the client sending a DNS query and ends with the client obtaining the IP address of the domain. For example, when a user enters `www.example.com` in a browser and presses enter, the domain resolution process begins. This document assumes that BytePlus DNS provides authoritative DNS service for `www.example.com`.


1. The operating system checks whether there is a DNS record for `www.example.com` in the local `hosts` file. If the operating system finds a DNS record for `www.example.com` in the `hosts` file, it will use the IP address in that record. At this point, DNS resolution is complete.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In general, the operating system first checks the local <code>hosts</code> file. However, this order is not absolute. The operating system may also first query the local DNS cache.</div>


<div data-tips="true" data-tips-type="tip">The <code>hosts</code> file in Windows is located in the <code>%Windir%\System32\drivers\etc</code> directory, and the hosts file in macOS and Linux is located in the <code>/etc</code> directory.</div>



2. If there is no DNS record for `www.example.com` in the hosts file, the operating system will look for it in the local DNS cache. If the operating system finds a DNS record for `www.example.com` in the local DNS cache, it will use the IP address in that record. At this point, DNS resolution is complete.

3. If there is no DNS record for `www.example.com` in the local DNS cache, the operating system will send a DNS query to the recursive DNS server. A recursive DNS server can be a local DNS server maintained by the ISP or a public DNS server.

4. The recursive DNS server checks its cache. If the recursive DNS server finds a DNS record for `www.example.com` in its cache, it will return the IP address in that record. At this point, DNS resolution is complete.

5. If there is no DNS record for `www.example.com` in the cache of the recursive DNS server, the recursive DNS server will send a DNS query for the `.com` domain to the root DNS server.

6. The root DNS server returns the IP address of the corresponding top\-level domain DNS server to the recursive DNS server. The top\-level domain DNS server resolves the `.com` domain.

7. The recursive DNS server sends a DNS query for the `example.com` domain to the top\-level domain DNS server.

8. The top\-level domain DNS server returns the IP address of the corresponding authoritative DNS server to the recursive DNS server. The authoritative DNS server resolves the `example.com` domain. In this document, the authoritative DNS server for the `example.com` domain is provided by BytePlus DNS.

9. The recursive DNS server sends a DNS query to the authoritative DNS server.

10. The authoritative DNS server returns the IP address of `www.example.com` to the recursive DNS server.

11. The recursive DNS server returns the result to the user's operating system. At this point, DNS resolution is complete. The recursive DNS server will also cache the result for a period of time. The cache duration is the TTL (Time to Live) value of the DMS record. For subsequent DNS queries for www.example.com, the recursive DNS server will directly return the cached result.


The operating system returns the result to the browser. The browser sends an HTTP request to the IP address of `www.example.com`. Then, the user sees the content of the website.

The process of the operating system requesting DNS records from the recursive DNS server uses recursive queries. The process of the recursive DNS server requesting DNS records from domain servers at each level uses iterative queries.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_95b45fc20f5305c90c2766c127dfa0e3.jpeg) </span>

<span id="how-does-byteplus-dns-use-the-edns-client-subnet-ecs-protocol-to-obtain-the-ip-address-range-of-the-user-through-ecs"></span>
## How does BytePlus DNS use the EDNS Client Subnet(ECS) protocol to obtain the IP address range of the user through ECS?

If you have configured an ISP line, geolocation line, or IP\-based line for a DNS record, BytePlus DNS will prioritize using the partial client IP address included in the ECS protocol information in the DNS query to match the line.

<span id="if-the-local-dns-server-supports-the-ecs-protocol"></span>
### If the Local DNS server supports the ECS protocol

If the Local DNS server supports the ECS protocol, it sends the DNS query to BytePlus DNS with the ECS protocol information. BytePlus DNS will use the client IP address range included in the ECS protocol information in the DNS query to match the line.

<span id="if-the-local-dns-server-does-not-support-the-ecs-protocol"></span>
### If the Local DNS server does not support the ECS protocol

On the Internet, some Local DNS servers do not support the ECS protocol. If the Local DNS server does not support the ECS protocol, it sends the DNS query to BytePlus DNS without the ECS protocol information. BytePlus DNS will use the client IP address in the packet to match the line. Most of these client IP addresses are the egress IP addresses of the Local DNS server.
