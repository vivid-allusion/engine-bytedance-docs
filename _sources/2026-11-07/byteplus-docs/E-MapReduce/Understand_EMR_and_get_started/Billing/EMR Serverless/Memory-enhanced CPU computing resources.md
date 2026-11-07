---
title: "Memory-enhanced CPU computing resources"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Memory-enhanced_CPU_computing_resources"
---

Memory\-enhanced computing resources. The resource specification is 1 CU = 1 vCPU and 8 GiB Mem, which is suitable for complex numerical calculation scenarios with high memory requirements and memory\-intensive applications.

<span id="67bf3f1e"></span>
## **Billing standard**


|**Memory\-Enhanced CPU Computing Resources** |||||||
|---|---|---|---|---|---|---|
|**Payment methods** |**Sales Region** |**Billing unit** |**Resource specification** |**Rate card price** |**Unit** |**Queue type/Engine type** |
|Pay\-as\-you\-go |Asia Pacific (Johor) |CU·hour |1 CU = 1vCPU 8GiB Memory |$0.16 |CU/hour |* Public Queue<br><br>* Dedicated Queue (Elastic Resources) |
|Annual/Monthly Subscription |Asia Pacific (Johor) |CU/month ||$70 |CU/month |* Exclusive queue |


<span id="b96e815c"></span>
## Completely pay\-as\-you\-go  **(Whitelist)** 

<span id="77cedf19"></span>
### Serverless queues (Spark, Ray, Hive)

After the job **runs successfully**, the system will calculate the computing hours consumed by the job, summarize the detailed data that has been calculated every hour, and then calculate the cost.


* The job queuing time is not billed.

* The cost of the same job may fluctuate due to different specified resource sizes.


<span id="9bbd574f"></span>
#### Case estimation

The calculation model is as follows (domestic):


* Assume that the job submitted to the public queue continues to use 2 vCPUs and 16 GiB of memory and runs for 4 hours.


**Cost Estimation**:


|Billing methods |Cost |Description |
|---|---|---|
|Computing resources \- pay\-as\-you\-go |$1.28 = 8 CU·h × $0.16 CU/h |Postpaid |


The CU·hour calculation formula: MAX(2×1, ceiling(16×1/8)) CU × 4 hours = 8 CU·hours.

<span id="cc39c56b"></span>
## Subscription

This scenario only includes **the completely fixed annual/monthly subscription model**. To use this form of resources, purchase **instances/dedicated queues**. Pay according to the amount of resources configured when purchasing the queue. The specific unit prices and descriptions are as follows:

<span id="010deec2"></span>
### Serverless Queue

<span id="d2941173"></span>
#### Case Estimation

The calculation model is as follows (domestic):

Assume that when the user chooses to purchase an annual/monthly subscription, a queue specification of 128 CU is configured and used for 1 month. Then this part of the resources needs to be calculated according to the annual/monthly subscription.

**Cost Estimation:** 


|Billing methods |Cost |Description |
|---|---|---|
|Computing resources \- Subscription |$8960 = 128 CU × $70 CU/month × 1 month |Prepaid |


<span id="7cfb9646"></span>
## Hybrid billing

This scenario includes both **annual/monthly subscription and pay\-as\-you\-go models**. Purchasing **an exclusive queue and enabling elastic resources** allows you to use these two resource forms in one queue. The annual/monthly subscription is prepaid, and the elastic pay\-as\-you\-go is postpaid. The specific unit prices and descriptions are as follows:

<span id="2ae01069"></span>
### Serverless Queue

<span id="9d7ac52d"></span>
#### Case Estimation

Assume the calculation model is as follows:

Assume that the user purchases an annual/monthly subscription and selects elastic resources, and configures a queue with a MIN value of 128 CU and a MAX value of 256 CU. The resources for the MIN value part need to be calculated based on the annual/monthly subscription. The part from the MIN value to the MAX value (128, 256] is billed according to the actual usage (sum of hours).

**Cost Estimation:** 


|Billing methods |Cost |Description |
|---|---|---|
|Computing costs \- Subscription |$8960 = 128 CU × $70 CU/month × 1 month |Prepaid |
|Computing costs \- Pay\-as\-you\-go |$x。 Unit price: $0.16 CU/hour |Postpaid |
|Total cost |$8960 + $x |— |
