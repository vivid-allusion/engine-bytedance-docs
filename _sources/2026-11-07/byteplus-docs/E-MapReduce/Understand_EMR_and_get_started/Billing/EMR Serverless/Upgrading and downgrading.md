---
title: "Upgrading and downgrading"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Upgrading_and_downgrading"
---

<span id="dadb434f"></span>
## More instructions

<span id="17288097"></span>
### EMR Serverless Queue

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Pay\-as\-you\-go does not support more allocation. The annual subscription and monthly instances support more allocation, and the number of CUs can be modified. You can modify the configuration of the queue according to the load of the actual business.</div>



* If it is an upgrade, the price difference needs to be calculated according to the value of the configuration before and after (the new configuration price \- the residual value of the old configuration), and the price difference can be paid. Old configuration residual value = old configuration remaining time (days)/order purchase time (days) \* order amount actually paid.

* If it is a reduction, **only the remaining amount will be returned, and the voucher cannot be returned.** 

   * Under the scenario of annual package and monthly package, the usage time is < 30 days: the refund amount is reduced = the real value of the order \- the monthly issue price at the time of purchase \* [usage time (day)/(365/12) ] \* applicable discount \* **1.5** \* [real value of the order/(real value of the order + voucher deduction amount) ]

   * Under the scenario of annual package and monthly package, the use time is ≥ 30 days: the refund amount is reduced = the real value of the order \- the monthly publication price at the time of purchase \* [the use time (days)/(365/12) ] \* the applicable discount \* [the real value of the order/(the real value of the order + the deduction amount of the voucher) ]
