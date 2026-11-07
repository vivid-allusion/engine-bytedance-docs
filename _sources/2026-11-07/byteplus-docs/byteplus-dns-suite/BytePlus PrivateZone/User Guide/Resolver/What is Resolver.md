---
title: "What is Resolver"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/6X0ngX"
---

In BytePlus PrivateZone, the Resolver can provide the following services:


* Provide recursive DNS services for DNS queries from within VPCs and DNS queries forwarded to the resolver through inbound endpoints.

   * For DNS queries that match DNS records, the resolver will return cached DNS records or obtain DNS response from the authoritative DNS server.

   * For DNS queries that match recursive DNS, the resolver will obtain DNS response from a public recursive DNS server.

* For DNS queries that match rules, forward the DNS queries to external DNS servers through rules and outbound endpoints.
