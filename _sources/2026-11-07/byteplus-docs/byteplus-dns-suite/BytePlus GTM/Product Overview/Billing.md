---
title: "Billing"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/R4Anoj"
---

This document introduces the billing of BytePlus GTM.

BytePlus GTM contains the following pricing components:


* GTM instance

* Serving DNS queries

* Health check



|**Billing item** |**Billing method** |**Billing cycle** |**Unit price** |
|---|---|---|---|
|GTM instance |Pay\-as\-you\-go |Daily (For monthly billing, please contact sales) |* Standard Edition: $0.014 / Per GTM instance / Per day<br><br>* Ultimate Edition: $0.14 / Per GTM instance / Per day |
|Serving DNS queries |Pay\-as\-you\-go |Daily (For monthly billing, please contact sales) |$0.0086 / 10,000 DNS queries |
|Health check |Pay\-as\-you\-go |Daily (For monthly billing, please contact sales) |* 1\-minute interval: $0.006 / Per health check task / Per day<br><br>* 15\-second interval: $0.024 / Per health check task / Per day |


<span id="billing-example"></span>
## Billing example

Assume BytePlus account A has added three GTM instances of standard edition: `1.example.com`, `2.example.com`, `3.example.com`.

Over one day, account A's three GTM instances serve a total of 100,000 DNS queries, and account A has 100 health check tasks in total. Among these health check tasks, 50 are set at 1\-minute intervals and the other 50 are set at 15\-second intervals.

The total cost for account A for one day would be: $1.628 = $0.042 (Fee of GTM instances, $0.014 \* 3) + $0.086 (Fee of serving DNS queries, $0.0086 \* 10) + $1.5 (Health check fees, $0.006 \* 50 + $0.024 \* 50).

<span id="billing-cycle"></span>
## Billing cycle


* Daily billing cycles: Bills for the previous day's fees are issued daily.

* Monthly billing cycles: Bills for the previous month's fees are issued on the first four business days of the month.


<span id="service-suspension-due-to-arrears"></span>
## Service suspension due to arrears


* If you do not pay off all outstanding bills within 72 hours of being in arrears, BytePlus temporarily suspends the service of your GTM instance.

* If all outstanding bills are paid within 720 hours of the arrears, the service of your GTM instance will be restored.

* If the arrears exceed 720 hours, your GTM instance will be released, all data related to your GTM instance will be deleted and cannot be recovered.
