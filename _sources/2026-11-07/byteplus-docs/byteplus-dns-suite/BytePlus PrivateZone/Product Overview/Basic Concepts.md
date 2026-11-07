---
title: "Basic Concepts"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/xsDets"
---

This document introduces the fundamental concepts of the domain name system (DNS) for BytePlus PrivateZone.

<span id="vpc"></span>
## VPC

A Virtual Private Cloud (VPC) provides a logically isolated, customizable virtual network environment for BytePlus cloud resources. See [What is VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC).

<span id="authoritative-dns-server"></span>
## Authoritative DNS server

An authoritative DNS server is a server that maintains resource records. An authoritative DNS server does not directly receive DNS queries from users, but interacts with recursive DNS servers. When receiving a DNS query from a recursive DNS server, the authoritative DNS server returns authoritative resource records.

<span id="recursive-dns-server"></span>
## Recursive DNS server

A recursive DNS server (Recursive Server) receives DNS queries from users. If a user's DNS query hits the cache, the recursive DNS server returns the cached resolution result. If a user's DNS query does not hit the cache, the recursive DNS server obtains the resolution result from authoritative DNS servers through iterative queries. The recursive DNS server returns the resolution result to the user and caches it.

<span id="resolver"></span>
## Resolver

In BytePlus PrivateZone, the Resolver can provide the following services:


* Provide recursive DNS services for DNS queries from within VPCs and DNS queries forwarded to the resolver through inbound endpoints.

   * For DNS queries that match DNS records, the resolver will return cached DNS records or obtain DNS response from the authoritative DNS server.

   * For DNS queries that match recursive DNS, the resolver will obtain DNS response from Internet's Local DNS server.

* For DNS queries that match rules, forward the DNS queries to external DNS servers through rules and outbound endpoints.


<span id="rules"></span>
## Rules

Rules are used to forward DNS queries to external DNS servers. A rule specifies the domain names for which DNS queries need to be forwarded, the corresponding outbound endpoints, and the IP addresses of external DNS servers. You create rules in the resolver.

Only DNS queries that come from VPCs within the effective range of the rule and match the forwarding domain of the rule will be forwarded according to the rule.

<span id="outbound-endpoints"></span>
## Outbound Endpoints

Outbound endpoints are the exit points for DNS queries. In scenarios where DNS queries are forwarded to external DNS servers, you need to create outbound endpoints.

<span id="outbound-vpc"></span>
## Outbound VPC

In scenarios where DNS queries are forwarded to external DNS servers, you need to create an outbound VPC. The outbound VPC is used to establish network connections with self\-built IDC/third\-party cloud services.

<span id="inbound-endpoints"></span>
## Inbound Endpoints

Inbound endpoints are the entry points for DNS queries. In scenarios where external DNS queries are forwarded to the resolver, you need to create inbound endpoints.

<span id="inbound-vpc"></span>
## Inbound VPC

In scenarios where external DNS queries are forwarded to the resolver, you need to create an inbound VPC. The inbound VPC is used to establish network connections with self\-built IDC/third\-party cloud services.

<span id="domain-name"></span>
## Domain name

Within DNS, a domain name identifies network resources in the domain name space. A domain name comprises a root domain, top\-level domain, second\-level domain, and optionally subdomains. For example, in `www.volcengine.com.`, the top\-level domain is `com`, the second\-level domain is `volcengine`, the subdomain is `www`, and the root domain is `.`. The root domain is commonly omitted in domain notation.

Refer to [RFC 1034](https://datatracker.ietf.org/doc/rfc1034/) and [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/) for detailed information.

Within a VPC, domain names can identify resources like ECS, TOS, or RDS. For example, `ecs-game-app-huabei1.private.zone.` could signify the private network IP address of an ECS.

<span id="resource-record"></span>
## Resource record

In BytePlus PrivateZone, a resource record (RR) maps domain names to resource information within the VPC. For instance, the following record specifies that the domain `example.com` corresponds to the internal IPv4 address 10.0.0.1.

```Plain
@.example.com.           600           IN    A        10.0.0.1
```


Refer to [RFC 1034](https://docs.byteplus.com/docs/6758/1108549) and [RFC 1035](https://docs.byteplus.com/docs/6758/1108549) for more details.

<span id="record-set"></span>
## Record set

BytePlus PrivateZone uses record sets (RRSet) to manage one or more resource records with the same domain name, traffic routing line, and type. You can assign weights to multiple resource records within a record set to achieve DNS\-based load balancing. See RRSet in [RFC 7719](https://www.rfc-editor.org/rfc/rfc7719.html).

<span id="record-value"></span>
## Record value

The record value (RDATA) is the resource data within a resource record. For example, the resource record below designates the IPv4 address for the domain name `example.com` as `10.1.1.1`, where `10.1.1.1` represents the record value.

```Plain
@.example.com.           600           IN    A        10.1.1.1
```


Refer to [RFC 1034](https://datatracker.ietf.org/doc/rfc1034/) and [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/) for detailed information.

<span id="hostname-record"></span>
## Hostname record

BytePlus PrivateZone can automatically generate a DNS record based on the hostname of each ECS instance, which is the hostname record. Each hostname record corresponding to an ECS instance points to the internal IP address of that ECS instance. This way, you can access the ECS instance through the hostname record.

<span id="line"></span>
## Line

Lines indicate the source of user requests. In BytePlus PrivateZone, a line can be a VPC subnet.

If your domain can be resolved to different service IP addresses, and you want user requests to be routed to an IP address that meets the following requirement to reduce user access latency:


* The VPC subnet of the user's IP address is the same as the VPC subnet of the service IP address.


You can assign a line to a record set that contains one or multiple service IP addresses. Each line represents the VPC subnet of the service IP addresses in the record set.

When the DNS server of BytePlus PrivateZone receives a DNS query, it determines the VPC subnet of the client's IP address based on the client IP address included in the DNS query. If the client's VPC subnet matches the line, the DNS response will only include the IP addresses within the corresponding record set.
