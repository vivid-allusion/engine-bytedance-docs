---
title: "Billing rules"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-rules"
---

<span id=".6K6h6LS56aG5"></span>
## Billing item

The BytePlus Application Load Balancer (ALB) billing items include instance fee, Load Balancer Capacity Unit (LCU) fee, and public network fee (only applicable to internet\-facing instances).


* Instance fee: the usage fee for ALB instances.

* Load Balancer Capacity Unit (LCU) fee: LCU is a performance metric for ALB instances handling traffic. ALB charges according to metric data. See the billing rules for details at [Load Balancer Capacity Unit (LCU) fee](https://docs.byteplus.com/docs/clb/Billing-rules#.5oCn6IO95a656YeP5Y2V5YWDLWxjdS3otLk=).

* Public network fee: if you create an internet\-facing ALB instance, it communicates over the internet through a public IP. Public network fees are charged according to the billing method for public IP. See [Public IP billing notes](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go) for details.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you create a VPC ALB instance, no public network fee applies.   </div>
   

<span id=".5a6e5L6L6LS5"></span>
## Instance fee

<span id=".6K6h6LS55o-P6L-w"></span>
### Billing description


* ALB instances use a pay\-as\-you\-go billing method.

* ALB instances are billed by usage time, with a billing cycle of 1 hour. The system generates the previous hour's bill every hour and deducts the amount accordingly.

* The unit price and fee calculation formula for ALB instances are as follows:



|Instance edition |Instance unit price |Cost formula for a single instance |
|---|---|---|
|Basic edition |USD 0.007 per hour |Instance charge = unit price per instance (USD/h) × billing duration (h) |
|Standard edition |||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance usage within a billing cycle is less than 1 hour, the system charges proportionally based on the actual usage time.</div>


<span id=".6K6h6LS556S65L6L"></span>
### Billing example

If you create a VPC ALB instance at 00:00:00 on 2021\-03\-01 and use it normally, the instance charge generated at 01:00:00 on 2021\-03\-01 is: 0.007 × 1 = USD 0.007.

<span id=".5oCn6IO95a656YeP5Y2V5YWDLWxjdS3otLk="></span>
## Performance Capacity Unit (LCU) fee

<span id=".bGN1Leamgui_sA=="></span>
### LCU Overview

LCU is a performance metric for ALB instance business processing, including four dimensions of performance metrics, as detailed in the table below.


|**metric** |**Definition** |**Performance metric values included in a single LCU** |**LCU number calculation** |
|---|---|---|---|
|New Connections Per Second(CPS) |Average number of new connections processed per second. |25 per second |Number of LCUs = average new connections per second handled by the ALB instance during the billing cycle ÷ 25 |
|number of concurrent connections |Average number of concurrent connections per minute. |3,000 per minute |Number of LCU = average number of concurrent connections processed per minute by ALB instance during billing cycle ÷ 3000 |
|traffic |Total data transfer for ALB instances, including:<br><br><br>* Incoming traffic: the amount of data generated when clients send requests to ALB instances.<br><br>* Outgoing traffic: the amount of data generated when ALB instances return responses to clients. |1 GB per hour |Number of LCUs = Total inbound and outbound data transfer processed by the ALB instance during the billing cycle ÷ 1 |
|Rule evaluations |The total number of forwarding rules handled by the ALB instance multiplied by the requests per second (QPS). Each instance has a free quota of 30 forwarding rules.<br><br><br>* When the number of forwarding rules handled by the instance does not exceed the free quota (30): rule evaluations = QPS.<br><br>* When the number of forwarding rules handled by the instance exceeds the free quota (30): rule evaluations = QPS × (number of forwarding rules − 30). |1000 per second |Number of LCUs = number of rule evaluations handled by the ALB instance during the billing cycle ÷ 1000 |


<span id=".6K6h6LS55o-P6L-w"></span>
### Billing description


* LCU uses a pay\-as\-you\-go billing method.

* LCU is billed based on usage time, with a billing cycle of 1 hour. The system generates the previous hour’s bill every hour and deducts the corresponding amount.

* Within one billing cycle, LCU quantities are calculated from four metric dimensions, and the largest value is used as the billing measurement.

* The unit price and fee calculation formula for LCU are as follows:



|LCU unit price |LCU billing formula for a single instance |
|---|---|
|USD 0.007/LCU |LCU fee per hour = LCU unit price (USD/unit) × LCU metered quantity (unit) |


<span id=".6K6h6LS556S65L6L"></span>
### Billing example

If you create a VPC ALB instance at 00:00:00 on 2021\-03\-01 and the instance is used normally, the LCU metrics and corresponding LCU quantities for this instance within one hour after 01:00:00 on 2021\-03\-01 are as follows:


|LCU metric ||statistics |Number of LCU |
|---|---|---|---|
|New Connections Per Second ||100 |Number of LCUs for new connections = 100 ÷ 25 = 4 |
|Number of concurrent connections ||18,000 |Number of concurrent connections LCU = 18000 ÷ 3000 = 6 |
|traffic ||3.6 GB |Traffic LCUs = 3.6 GB ÷ 1 GB = 3.6 units |
|Rule evaluations |QPS |400 |Number of rule evaluations LCU = 400 × (32 \- 30) ÷ 1000 = 0.8 |
||Number of forwarding rules on the instance |32 ||


The LCU billing measurement for this instance during this billing cycle is 6 units, generating an LCU fee of: 0.007 × 6 = USD 0.042.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to pay\-as\-you\-go resources, ALB also offers prepaid resource packages. After you purchase a resource package, the system will automatically deduct business usage from the package at settlement. Compared to the pay\-as\-you\-go method, ALB resource packages offer greater discounts. If your company requires prepaid services, consider purchasing a resource package. For more information, refer to <a href="https://docs.byteplus.com/docs/clb/Resource-packages">Resource Package</a>.</div>
