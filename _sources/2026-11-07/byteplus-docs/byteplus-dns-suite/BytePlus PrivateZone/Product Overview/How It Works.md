---
title: "How It Works"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/W8AW7y"
---

This document introduces how BytePlus PrivateZone works.

The resolver of BytePlus PrivateZone can respond to DNS queries from VPCs or inbound endpoints. Upon receiving a DNS query, the resolver attempts to respond using authoritative, forwarding, or recursive methods in the following order:


1. **Authoritative**: The resolver attempts to match the DNS query to a domain name.

   * If successful, the resolver obtains the DNS response from the authoritative DNS server. If recursive DNS is enabled for the domain, and the authoritative DNS server cannot find a DNS record, the resolver will use the recursive DNS proxy as a fallback. See step 3.

   * If unsuccessful, proceed to step 2.

2. **Forward**: The resolver attempts to match the DNS query to a rule of type **Forward DNS queries to an external DNS server**.

   * If successful, the resolver forwards the DNS query to an external DNS server (such as on\-premise data center or third\-party cloud service) according to the rule, and returns the DNS response from the external DNS server.

   * If unsuccessful, proceed to step 3.

3. **Recursive**: The resolver checks if the DNS query meets the effective conditions for the recursive DNS proxy.

   * If the DNS query meets the effective conditions for the recursive DNS proxy, the resolver acts as a recursive DNS proxy to obtain the DNS response from a public recursive DNS server.

   * If the DNS query does not meet the effective conditions for the recursive DNS proxy, DNS resolution fails.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ab6155eeb06c8ca72395a79ebaf114b5.jpeg) </span>

<span id="1107f679"></span>
## How BytePlus PrivateZone handles DNS queries

After receiving a DNS query, the resolver attempts to respond using authoritative, forwarding, or recursive methods in the following order:


1. **The resolver attempts to respond to the DNS query by the authoritative method**: The resolver determines whether the DNS query matches a domain. See [How the resolver determines whether a DNS query matches a domain](https://docs.byteplus.com/docs/byteplus-dns-suite/W8AW7y#aee5f5f9).

   * If a matching domain is found, the resolver first searches the cache for DNS records of the matched domain.

      * If a DNS record is found in the cache, the resolver returns the found records. At this point, DNS resolution is complete.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">If intelligent DNS or load balancing is enabled for the domain, the DNS records for that domain will not be cached.         </div>
         

      * If no DNS record is found in the cache, the resolver sends a DNS query to the authoritative DNS server of BytePlus PrivateZone.

         * If the authoritative DNS server finds a DNS record, it returns the found record to the resolver. The resolver returns the DNS record to the client and saves it in the cache. At this point, DNS resolution is complete.

         * If the authoritative DNS server does not find a DNS record, the resolver determines if recursive DNS is enabled for the domain:

            * If recursive DNS is enabled for the domain, the resolver will use the recursive DNS proxy as a fallback. At this point, the DNS query will successfully meet the effective conditions for the recursive DNS proxy. See step 3.

            * If recursive DNS is not enabled for the domain, DNS resolution fails.

   * If no matching domain is found, the resolver proceeds to the next step.

2. **The resolver attempts to respond to the DNS query by the forward method**: The resolver determines if the DNS query matches a rule of type **Forward to external DNS system**. See [How the resolver determines if a DNS query matches a rule](https://docs.byteplus.com/docs/byteplus-dns-suite/W8AW7y#d834cf31).

   * If a matching rule is found, the resolver first checks the cache for DNS records obtained according to the rule.

      * If a DNS record is found in the cache, the resolver returns the found record. At this point, DNS resolution is complete.

      * If no DNS record is found in the cache, the resolver forwards the DNS query to the external DNS server according to the matched rule, then returns the DNS response from the external DNS server to the client. At this point, DNS resolution is complete.

   * If no matching rule is found, the resolver proceeds to the next step.

3. **The resolver attempts to respond to the DNS query by the recursive method**: The resolver determines if the DNS query meets the effective conditions for the recursive DNS proxy . See [How the resolver determines whether a DNS query matches a rule](https://docs.byteplus.com/docs/byteplus-dns-suite/W8AW7y#3eed3010).

   * If the DNS query meets the effective conditions for the recursive DNS proxy , the resolver first checks the cache for DNS records from the public recursive DNS server.

      * If a DNS record is found in the cache, the resolver returns the found record. At this point, DNS resolution is complete.

      * If no DNS record is found in the cache, the resolver returns the query result obtained from the public recursive DNS server. The resolver also saves this record in the cache. At this point, DNS resolution is complete.

   * If the DNS query does not meet the effective conditions for the recursive DNS proxy , DNS resolution fails.


The following diagram shows how BytePlus PrivateZone handles DNS queries.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c333342c927b402c4d73036b89a57321.png) </span>

<span id="4dcc00d9"></span>
## How the resolver determines whether a DNS query matches a domain, rule, or meets the effective conditions for the recursive DNS proxy

<span id="aee5f5f9"></span>
### How the resolver determines whether a DNS query matches a domain

For DNS queries from VPCs associated with a domain, if the domain in the DNS query is the same as or a subdomain of the domain, then the DNS query successfully matches the domain.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The matching process between DNS queries and domains follows the longest suffix matching principle. For example, if the domain in the DNS query is <code>123.abc.example.com</code>, and BytePlus PrivateZone has both <code>example.com</code> and <code>abc.example.com</code> domains, then the DNS query will match the domain <code>abc.example.com</code>.</div>


<span id="d834cf31"></span>
### How the resolver determines whether a DNS query matches a rule

For DNS queries from VPCs associated with a rule, if the domain in the DNS query is the same as or a subdomain of the domain associated with the rule, then the DNS query successfully matches the rule.

For example, if the domain associated with a rule is `example.com`, then the rule can successfully match when the domain in the DNS query is `example.com`, `abc.example.com`, or `1234.abc.example.com`.

<span id="3eed3010"></span>
### How the resolver determines whether a DNS query meets the effective conditions for the recursive DNS proxy

If the DNS query meets any of the following conditions, then it meets the effective conditions for the recursive DNS proxy :


* The domain in the DNS query does not match any domain in BytePlus PrivateZone, nor does it match any rule of type **Forward DNS queries to an external DNS server**.

* The domain in the DNS query matches a domain in BytePlus PrivateZone. This domain has recursive DNS enabled, and the domain in the DNS query does not match any DNS record under the domain. For example, the domain in the DNS query is `www.example.com`, and BytePlus PrivateZone has a domain `example.com`, but none of the DNS records under this domain match `www.example.com`.
