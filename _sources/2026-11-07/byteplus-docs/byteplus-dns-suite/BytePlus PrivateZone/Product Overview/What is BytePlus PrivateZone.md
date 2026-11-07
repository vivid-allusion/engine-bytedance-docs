---
title: "What is BytePlus PrivateZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/roaUXT"
---

BytePlus PrivateZone provides DNS services for [BytePlus Virtual Private Cloud (VPC)](https://www.byteplus.com/en/product/vpc). BytePlus PrivateZone can achieve the following functions through its built\-in recursive DNS service, authoritative DNS service, DNS forwarding service, and DNS outbound recursive service:


* Resolve domain names to IP addresses within VPC or public IP addresses

* Forward DNS queries between VPC and on\-premise IDC/third\-party cloud services


<span id="feature-overview"></span>
## Feature overview

BytePlus PrivateZone supports the following features.

<span id="recursive-dns-service-and-authoritative-dns-service"></span>
### Recursive DNS service and Authoritative DNS service

BytePlus PrivateZone provides recursive DNS service and authoritative DNS service for VPC. DNS queries from VPC are first received by the recursive DNS server:


* If the cache in the recursive DNS server matches the queried domain name of the DNS query, the recursive DNS server will return the DNS record from the cache.

* If the cache in the recursive DNS server does not have the queried domain name of the DNS query, the recursive DNS server will send a DNS query to the authoritative DNS server and return the query result from the authoritative DNS server.


BytePlus PrivateZone also supports subnet\-based routing, load balancing, and import/export and backup of DNS records.


* **Subnet\-based routing**: Allows you to select the service address corresponding to the domain name based on the subnet where the client is located.

* **Load balancing**: If a record set contains multiple record values, and each record value has a weight, BytePlus PrivateZone will calculate the sum of weights for all record values in the record set and determine the weight proportion of each record value. Based on the weight proportion of each record value, BytePlus PrivateZone will return that record value when responding to the same proportion of DNS queries.

* **Import/Export and backup of DNS records**: You can import external DNS records into BytePlus PrivateZone, and you can also export DNS records from BytePlus PrivateZone to files. Additionally, you can backup DNS records.


<span id="dns-forwarding-service"></span>
### DNS forwarding service

BytePlus PrivateZone provides DNS forwarding service, which can forward DNS queries from VPC to DNS servers in on\-premise IDC/third\-party cloud services, and can also forward DNS queries from on\-premise IDC/third\-party cloud services to the recursive DNS server of BytePlus PrivateZone.

<span id="outbound-recursive-dns-service"></span>
### Outbound recursive DNS service

In addition to resolving domain names to IP addresses within VPC, BytePlus PrivateZone can also forward DNS queries to recursive DNS servers on the Internet and return the query results from these Internet recursive DNS servers.

<span id="view-dns-query-statistics"></span>
### View DNS query statistics

You can view statistics on DNS queries resolved by recursive DNS service and authoritative DNS service, forwarded DNS queries, and DNS queries resolved by outbound recursive DNS service. These statistics can be categorized by traffic type, DNS response, record type, ISP, geolocation, and other dimensions.
