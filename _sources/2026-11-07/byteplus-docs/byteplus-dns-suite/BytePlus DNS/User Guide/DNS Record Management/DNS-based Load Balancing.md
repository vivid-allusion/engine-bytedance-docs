---
title: "DNS-based Load Balancing"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-load-balancing-with-weighted-dns-records"
---

This document describes how to implement DNS\-based load balancing in BytePlus DNS.

<span id="feature-overview"></span>
## Feature Overview

If a record set contains multiple record values, and each record value has a weight, BytePlus DNS will calculate the sum of all record values' weights in the record set and determine the weight proportion of each record value. Based on these proportions, BytePlus DNS will return the corresponding record value when responding to DNS queries at the same ratio.

For example, if `www.example.com` has a record set with two record values `203.0.113.1` and `203.0.113.2`, with weights of 1 and 3 respectively. If BytePlus DNS receives 100 DNS queries matching this record set, 25 DNS query responses will contain the record value `203.0.113.1`, and 75 DNS query responses will contain the record value `203.0.113.2`.


* In the BytePlus DNS console, BytePlus DNS automatically manages record sets for you. You can create multiple record values for a single DNS record. Then, you can implement DNS\-based load balancing by setting weights for the record values.

* In the BytePlus DNS OpenAPI, you can implement DNS\-based load balancing through record sets.


BytePlus DNS has the following limitations for load balancing:


* For A and AAAA type records, you can enable or disable load balancing. When load balancing is disabled, BytePlus DNS will return all record values upon receiving a DNS query. The order of record values is random.

* For TXT, MX, SRV, NS, and CAA type records, load balancing is disabled by default and cannot be enabled.

* BytePlus DNS automatically enables load balancing for CNAME records and sets default weights. You cannot disable load balancing for CNAME records. This ensures that even if you add multiple CNAME records, BytePlus DNS will only return one CNAME record each time.

* Refer to [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) for limitations on the number of DNS records in a record set and the range of weight values in BytePlus DNS.


<span id="examples"></span>
## Examples


* If you set the weights of two record values to 4 and 1 respectively, 4/(4+1) = 80% of the traffic will be routed to the first record value, and 1/(4+1) = 20% of the traffic will be routed to the second record value.

* If you set the weights of three record values to 8, 6, and 3 respectively, 8/(8+6+3) = 47% of the traffic will be routed to the first record value, 6/(8+6+3) = 35% of the traffic will be routed to the second record value, and 3/(8+6+3) = 18% of the traffic will be routed to the third record value.


<span id="use-case"></span>
## Use Case

A common scenario is the gradual release of a new service. The new service has its own IP address. You can initially set a small weight for the new service, routing a small amount of traffic to the IP address of the new service. After monitoring and testing, you can gradually increase the weight to route more traffic to the IP address of the new service, eventually achieving full release of the new service.

Suppose your business domain is `test.example.com`. The IP address this domain points to is `203.0.113.1`. You need to gradually release a new service. The IP address of the new service is `203.0.113.2`. You want 22% of user traffic to be routed to `203.0.113.2`, and 78% of user traffic to be routed to `203.0.113.1`.

<span id="steps"></span>
### Steps

Follow the steps below to allocate user traffic according to the ratio in the example scenario. This document assumes that you have already added the domain name example.com and the corresponding DNS record `test.example.com` in BytePlus DNS Suite.


1. Open the **Edit records** page of the `test.example.com` DNS record. See [Create DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for details.

2. On the **Edit records** page, set the following parameters.


**Basic information**


|**Parameter** |**Description** |
|---|---|
|**Domain** |Set to `test`. |
|**Record type** |Set to **A**. |
|**TTL** |Set to **10 minutes**. |
|**Line** |Set to **Default line**. |
|**Load balancing** |Set to **Enable**. |


**Record value**


|**Record Value** |**Weight** |**Enable** |
|---|---|---|
|203.0.113.1 |78 |Enable |
|203.0.113.2 |22 |Enable |



3. After setting the parameters, click **Submit**.
