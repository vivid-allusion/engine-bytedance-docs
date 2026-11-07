---
title: "Limits"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/0K0WyX"
---

BytePlus PrivateZone currently do not differentiate between editions. The following limits apply for each BytePlus account:


|Number of domains |Number of VPCs associated per domain |Number of DNS records per domain |TTL |Load balancing |DNS request rate per ECS |
|---|---|---|---|---|---|
|Up to 500. |Up to 100. |* If recursive resolution is not enabled for your domain, there can be up to 100,000 DNS records per domain.<br><br>* If recursive resolution is enabled for your domain, there can be up to 4,000 DNS records per domain. |1 second to 86,400 seconds |A record set can contain up to 100 record values. The weight range for record values is 1 to 100. |Up to 5,000 requests per second. |


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If the DNS request rate per ECS exceeds 5,000 requests/second, BytePlus PrivateZone will throttle DNS requests. If your DNS requests are being throttled, BytePlus PrivateZone cannot guarantee an availability of less than 99.99% for private domain name resolution. Refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/AYq9fP">Reduce the DNS Query Frequency From an ECS Instance</a> for possible workarounds.</div>
