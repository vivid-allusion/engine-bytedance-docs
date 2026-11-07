---
title: "Billing"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/43T5hU"
---

This document introduces the billing of BytePlus PrivateZone.

BytePlus PrivateZone has the following pricing components:


* Authoritative DNS service: hosting domains and serving DNS queries

* Resolver: endpoint IP addresses and forwarding DNS queries


<span id="authoritative-dns-service"></span>
## Authoritative DNS service


|**Billing item** |**Billing method** |**Billing cycle** |**Unit price** |**Remarks** |
|---|---|---|---|---|
|Hosting domains |Pay\-as\-you\-go |Daily |$0.015 / Per domain / Per day |For domains that are created and then deleted in less than a day, DNS service fee for that domain will not be charged. |
|Serving DNS queries |Pay\-as\-you\-go |Daily |$0.004 / Per 10,000 DNS queries |Billed daily |


<span id="billing-example"></span>
### Billing example

BytePlus Account A has created three domains: `example1.local`, `example2.local`, and `example3.local`.

A total of 100,000 DNS queries are received for these three domains in one day.

The total cost for BytePlus Account A in one day is: $0.085 = $0.045 (fee of hosting domains, $0.015 \* 3) + $0.04 (fee of serving DNS queries, $0.004 \* 10).

<span id="number-of-dns-queries-as-a-billing-item"></span>
### Number of DNS queries as a billing item

DNS queries have a TTL caching mechanism. The number of DNS queries as a billing item refers to the number of DNS queries received by the authoritative DNS server.

For example, if the TTL for a domain `example.local` is set to 60 seconds, within the valid TTL period, all DNS queries from clients hit the cache of the recursive DNS server and do not incur charges. After the TTL expires, if there is one more DNS query from clients, the recursive DNS server sends a DNS query to the authoritative DNS server, and this DNS query is billed.


* The longer the TTL, the lower the frequency of DNS queries received by the authoritative DNS server, the slower DNS changes take effect, and the less the incurred costs.

* The shorter the TTL, the higher the frequency of DNS queries received by the authoritative DNS server, the faster the DNS changes take effect, and the more the incurred costs.


<span id="resolver-costs"></span>
## Resolver


|**Billing item** |**Billing method** |**Billing cycle** |**Unit price** |**Remarks** |
|---|---|---|---|---|
|IP addresses for outbound endpoints |Pay\-as\-you\-go |Hourly |$0.15 / Per IP address / Per hour |Billed hourly |
|Number of DNS queries forwarded by outbound endpoints |Pay\-as\-you\-go |Daily |$0.004 / Per 10,000 DNS queries |Billed daily |


<span id="billing-cycle"></span>
## Billing cycle


* If the billing cycle is on an hourly basis, a bill for the previous hour's fees is issued hourly.

* If the billing cycle is on a daily basis, a bill for the previous day's fees is issued daily.

* If the billing cycle is on a monthly basis, a bill for the previous calendar month's fees is issued within the first 4 business days of the month.


<span id="suspension-due-to-arrears"></span>
## Service suspension due to arrears


* If you do not pay off all outstanding bills within 72 hours of being in arrears, BytePlus temporarily suspends the service of your PrivateZone instance.

* If all outstanding bills are paid within 720 hours of the arrears, the service of your PrivateZone instance will be restored.

* If the arrears exceed 720 hours, your PrivateZone instance will be released, all data related to your PrivateZone instance will be deleted and cannot be recovered.
