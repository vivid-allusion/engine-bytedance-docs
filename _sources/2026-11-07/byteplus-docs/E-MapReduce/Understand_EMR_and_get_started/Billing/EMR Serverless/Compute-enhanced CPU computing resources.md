---
title: "Compute-enhanced CPU computing resources"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Compute-enhanced_CPU_computing_resources"
---

Compute\-enhanced computing resources. The resource specification is 1 CU = 1 vCPU and 2 GiB Memory. It is suitable for complex numerical computing scenarios with high computing requirements and compute\-intensive tasks.

<span id="fc7b6fe3"></span>
## **Billing standard**


|**Calculate enhanced CPU computing resources** |||||||
|---|---|---|---|---|---|---|
|**Payment methods** |**Selling Region** |**Billing unit** |**Resource specification** |**List price** |**Unit** |**Applicable scenario** |
|Pay\-as\-you\-go |Asia Pacific (Johor) |CU·hour |1 CU = 1vCPU 2GiB Memory |$0.11 |CU/hour |Public Queue<br><br>Dedicated Queue (Elastic Resources) |
|Annual/Monthly Subscription |Asia Pacific (Johor) |CU/month ||$45 |CU/month |Exclusive queue |


<span id="d18099e9"></span>
## Completely pay\-as\-you\-go  **(whitelist)** 

<span id="65304f15"></span>
### Serverless queue (applicable to Spark, Ray, and Hive queues)

After the job **runs successfully**, the system will calculate the computing hours consumed by the job, summarize the calculated detailed data every hour, and then calculate the cost.


* The job queuing time is not billed.

* The cost of the same job may fluctuate due to different specified resource sizes.


<span id="9a074f46"></span>
#### Case estimation

The computing model is as follows (domestic):


* Assume that the job submitted to the public queue continues to use 4 vCPUs and 8 GiB of memory and runs for 4 hours.


**Cost Estimation**:


|Billing methods |Cost |Description |
|---|---|---|
|Computing resources \- pay\-as\-you\-go |$1.76 = 16 CU · hour × $ 0.11 CU/hour |Postpaid |


The formula for CU·hour calculation: MAX(4×1, ceiling(8×1/2)) CU × 4 hours = 16 CU·hours.

<span id="312d55cf"></span>
## Subscription

This scenario only includes **a completely fixed annual/monthly subscription model**. Purchasing **instances/dedicated queues** allows you to use this form of resources. You will be charged according to the amount of resources configured when purchasing the queue. The specific unit prices and descriptions are as follows:

<span id="0ae01634"></span>
### Serverless Queue

<span id="e0ae276c"></span>
#### Case Estimation

The calculation model is as follows (domestic):


* Assume that when the user chooses to purchase an annual/monthly subscription, a queue specification of 128 CU is configured and used for 1 month. Then this part of the resources needs to be calculated according to the annual/monthly subscription.


**Cost estimate:** 


|Billing methods |Cost |Description |
|---|---|---|
|Computing resources \- Subscription |$5760 = 128 CU × $45 CU/month × 1 month |Prepaid |


<span id="8129dbd5"></span>
## Hybrid billing

This scenario includes both **annual/monthly subscription and pay\-as\-you\-go models**. Purchasing **a dedicated queue and enabling elastic resources** allows you to use these two resource forms in one queue. The annual/monthly subscription is prepaid, and the elastic pay\-as\-you\-go is postpaid. The specific unit prices and descriptions are as follows:

<span id="92f4e3a5"></span>
### Serverless queue

<span id="d1bb2709"></span>
#### Case estimate

Assume the calculation model is as follows:


* Assume the user purchases an annual/monthly subscription and selects elastic resources, and configures a queue with a MIN value of 128 CU and a MAX value of 256 CU. The resources for the MIN value part need to be calculated based on the annual/monthly subscription. The part from the MIN value to the MAX value (128, 256] is billed according to the actual usage (sum of hours of use).


**Cost estimate:** 


|Billing methods |Cost |Description |
|---|---|---|
|Calculating costs \- Subscription |$5760 = 128 CU × $45 CU/month × 1 month |Prepaid |
|Calculating costs \- Pay\-as\-you\-go |$x。 Unit price: $0.11 CU/hour |Postpaid |
|Total cost |$5760 + $x |— |
