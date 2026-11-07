---
title: "Basic Concepts"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-basicconcepts"
---

This document introduces the basic concepts of BytePlus DNS.

<span id="domain-name-system"></span>
## Domain name system

The domain name system (DNS) consists of the domain name space, resource records (RR), recursive DNS servers, and name servers (including root DNS servers, TLD DNS servers and authoritative DNS server). From the user's perspective, the DNS functions like a phone book, providing resource information for domain names.

For example, when users visits a website, they enter the website's domain name in the browser. The browser sends a DNS query to the DNS server. Upon receiving the DNS query, the DNS server resolves the domain name to an IP address and returns the IP address to the browser. Then, the browser sends an HTTP request to the IP address of the website server.

Refer to [RFC 1034](https://datatracker.ietf.org/doc/rfc1034/) and [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/) for detailed information.

<span id="domain-name"></span>
## Domain name

In DNS, domain names are used to identify network resources in the Domain Name Space. A domain name consists of the root domain, top\-level domain, site domain, and subdomain. For example, in `www.example.com`, the top\-level domain is `com`, the site domain is `example`, the subdomain is `www`, and the root domain is `.` (often omitted in domain names).

Refer to [RFC 1034](https://datatracker.ietf.org/doc/rfc1034/) and [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/) for detailed information.

<span id="resource-records"></span>
## Resource records

Resource records (RRs), or DNS records, map domain names to resource information. For example, the following resource record specifies that the domain name `example.com` corresponds to the IPv4 address `1.2.3.4`.

```Plain
@.example.com.           600           IN    A        1.2.3.4
```


Refer to [RFC 1034](https://datatracker.ietf.org/doc/rfc1034/) and [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/) for detailed information.

<span id="record-set"></span>
## Record set

BytePlus DNS uses record sets (RRSets) to manage one or more resource records with the same domain name, line, and type. You can set weights for multiple resource records in a record set to implement DNS\-based load balancing. See RRSet in [RFC 7719](https://www.rfc-editor.org/rfc/rfc7719.html) for more information.

<span id="record-value"></span>
## Record value

The record value (RDATA) is the resource information in a DNS record. For example, the following DNS record specifies that the domain name example.com corresponds to the IPv4 address 1.2.3.4. In this case, 1.2.3.4 is the record value of the resource record.

```Plain
@.example.com.           600           IN    A        1.2.3.4
```


Refer to [RFC 1034](https://datatracker.ietf.org/doc/rfc1034/) and [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/) for detailed information.

<span id="line"></span>
## Line

Lines indicate the source of user requests. A line can be defined by ISPs, geolocations, IP ranges, or combinations of ISPs, geolocations, and IP ranges.

If your domain can be resolved to different service IP addresses, and user requests are expected to be routed to an IP address that meet the following requirements to reduce user access latency:


* The ISP of the user's IP address is the same as the ISP of the service IP address.

* The geolocation of the user's IP address is as close to the geolocation of the service IP address.


You can assign a line to a record set that contains one or multiple service IP addresses. Each line represents the ISP, geolocation, or IP range of the service IP addresses in the record set.

When BytePlus DNS receives a DNS query, it gets the client's ISP, geolocation, IP address range, and other information based on the partial client IP address information included in the DNS query. If the client's ISP, geolocation or IP address range matches the line, only IP addresses within the corresponding record set will be included in the DNS response.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus DNS prioritizes using the client IP address range included in the ECS protocol information in the DNS query to match the line. If the user's local DNS server does not support the ECS protocol, BytePlus DNS uses the client IP address in the UDP packet. Most of these client IP addresses are the egress IP addresses of the local DNS server. Refer to <a href="https://docs.byteplus.com/byteplus-dns-suite/docs/how-it-works">How It Works</a> for more information.</div>


<span id="fqdn"></span>
## FQDN

FQDN (Fully Qualified Domain Name) represents the absolute name of a domain in DNS. Each domain's FQDN is unique in the DNS system. The FQDN includes all levels of the domain, including the root domain, such as www.example.com.

<span id="pqdn"></span>
## PQDN

PQDN (Partially Qualified Domain Name) represents the relative name of a domain in DNS, such as example.com.

<span id="root-domain"></span>
## Root domain

The root domain is the first level in a domain name, represented by a dot (.). The root domain is usually omitted in domain representations, but it is included in the FQDN of a domain name. There are 13 root domain DNS servers worldwide. Root domain DNS servers are responsible for domain name resolution of top\-level domains. Domain name resolution provides the IP addresses of top\-level domain DNS servers.

<span id="top-level-domain"></span>
## Top\-level domain

Top\-level domain (TLD) DNS servers obtain the IP addresses of authoritative DNS servers hosting site domains by resolving the domain names of site domains.

<span id="recursive-query"></span>
## Recursive query

A recursive query is a query mode of a DNS server. When a client initiates a DNS query, if the DNS server does not have a cached resource record, the DNS server acts as the client and sends a DNS query to other DNS servers, returning the result to the client. In a recursive query process, the client sends only one DNS query. A recursive DNS server responds to the client's DNS query using recursive queries.

<span id="name-server"></span>
## Name server

A name server (NS) is a server that stores resource records. Root DNS servers, top\-level domain DNS servers and authoritative DNS servers are all name servers.

<span id="authoritative-dns-server"></span>
## Authoritative DNS server

An authoritative DNS server is a server that maintains resource records. An authoritative DNS server does not directly receive DNS DNS querys from users, but interacts with recursive DNS servers. When receiving a DNS DNS query from a recursive DNS server, the authoritative DNS server returns authoritative resource records.

You can use BytePlus DNS to assign authoritative DNS servers for your public domains.

<span id="recursive-dns-server"></span>
## Recursive DNS server

A recursive DNS server receives DNS DNS querys from users. If a user's DNS DNS query hits the cache, the recursive DNS server returns the cached resolution result. If a user's DNS DNS query does not hit the cache, the recursive DNS server obtains the resolution result from authoritative DNS servers through iterative queries. The recursive DNS server returns the resolution result to the user and caches it.

A recursive DNS server can be a local DNS server or a public DNS server.

<span id="local-dns-server"></span>
## Local DNS server

A local DNS server is a type of recursive DNS server. Most local DNS servers are maintained by ISPs.

<span id="ecs-protocol-edns-client-subnet-protocol"></span>
## ECS protocol (EDNS Client Subnet Protocol)

The ECS protocol (EDNS Client Subnet Protocol) is a DNS extension protocol. Recursive DNS servers, such as local DNS servers, can send partial client IP address information to authoritative DNS servers through the ECS protocol. Based on the partial client IP address information, authoritative DNS servers can return the optimal resolution result.

BytePlus DNS supports the ECS protocol. Refer to [RFC 7871](https://tools.ietf.org/html/rfc7871) for detailed information about the ECS protocol.

<span id="dnssec"></span>
## DNSSEC

DNSSEC (DNS Security Extension) is a DNS extension protocol that authenticates DNS responses through asymmetric encryption, allowing verification of whether a DNS response originates from an authoritative DNS server. By enabling DNSSEC, the DNS system can prevent attacks such as DNS cache poisoning. In a DNS cache poisoning attack, an attacker sends DNS queries to a recursive DNS server while forging responses from an authoritative DNS server, thereby implanting incorrect IP addresses in the recursive DNS server's cache.

Each DNS zone has a public/private key pair, known as ZSK (zone Signing Keys). The owner of each zone uses the zone's private key to sign the DNS data within the zone. When a recursive DNS server queries a zone, it also retrieves the zone's public key and uses it to verify the digital signature of the DNS data. If the digital signature is valid, the recursive DNS server returns the DNS data to the user; if the digital signature is invalid, the recursive DNS server discards the DNS data and returns an error message. Thus, DNSSEC ensures the authenticity and integrity of DNS data.

However, the validity of each zone's public key itself needs to be ensured. Therefore, the owner of each zone also uses another public/private key pair (KSK, Key Signing Keys) to sign the zone's public key. The ZSK public key and KSK public key of each zone are signed by the zone's KSK private key. Additionally, to establish a chain of trust, the zone owner publishes the hash value of the KSK public key as a DS (Delegation Signer) record in the parent zone. The DS record, like other types of DNS records, is signed by the parent zone's ZSK private key, and the parent zone's ZSK public key is signed by its KSK private key. The parent zone owner also publishes the hash value of the KSK public key as a DS record in its parent zone, forming an effective chain of trust.

The root zone has no parent zone. The KSK (Root Key Signing Key) of the root zone is generated under the supervision of IANA. During IANA's [Key Signing Ceremony](https://www.iana.org/dnssec/ceremonies), the KSK private key of the root zone is used to sign the ZSK public key of the root zone.

Refer to [RFC 9364](https://datatracker.ietf.org/doc/html/rfc9364) for detailed information on DNSSEC.
