---
title: "Standard Computing Resources"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Standard_Computing_Resources"
---

CU/month

Standard computing resources, with resource specifications of 1 CU = 1 vCPU and 4 GiB Mem, are suitable for ordinary big data computing and query processing scenarios.

<span id="570b2a21"></span>
## **Standard Computing Resource Billing Standard**


|Standard CPU computing resources |||||||
|---|---|---|---|---|---|---|
|Payment method |Sales Region |billing unit |resource specification |**Unit price** |unit |Queue type/engine type |
|Pay\-As\-You\-Go |Asia Pacific (Johor) |CU · hour |1 CU = 1vCPU 4GiB Memory |$0.12 |CU/hour |* Public queue: Spark/Ray<br><br>* Exclusive queue (elastic section) |
|Subscription |Asia Pacific (Johor) |CU ||$50 |CU/month |* exclusive queue |
|Pay\-As\-You\-Go |Asia Pacific (Johor) |Scan volume by data |— |0.0001 |$/MB |* Public queue: Presto |


<span id="575407b4"></span>
## Pay\-As\-You\-Go (Postpaid)

<span id="2be73ff5"></span>
### Serverless Queue (Spark、Ray)

When the job **runs successfully** , the system counts the computation time consumed by the job, summarizes the detailed data that has been counted every hour, and then calculates the cost.


* Homework queuing time is not billed.

* The same job can have cost fluctuations due to differences in the size of the specified resource.


**Case estimate**

**The calculation model is as follows (Asia Pacific (Johor)):** 

Assume that job execution submitted to the public queue continues to use 2 vCPUs and 10 gigabytes of memory for 4 hours.

**Cost estimate** :


|**Billing method** |**cost** |**explain** |
|---|---|---|
|Pay\-As\-You\-Go |$1.44 = 12CU · hour × $0.12/CU/hour |postpaid |


CU · hour calculation formula: `MAX (2 × 1, rounded up (10 × 1/4))`CU × 4 = 12 CU · hour.

<span id="27d9ffe0"></span>
### Serverless Queue (Presto)

After all Presto SQL queries are successfully run, the system counts the storage of all the data scanned during job execution (regardless of complexity), summarizes the values of all the tasks of the previous day on a daily basis, and then calculates the cost.


* SQL queries that fail to execute are not billed.

* The scan metering caliber for SQL jobs is calculated based on the size of the compressed data.


**Case estimate**

**The calculation model is as follows (Asia Pacific (Johor)):** 

```SQL
Select * from order_table where dt <='2024-03-03' and dt >='2024-03-01'
Plain
```


**Cost estimate:** 

The hit partition range is 2024\-03\-01, 2024\-03\-02, 2024\-03\-03, the storage occupied by these three partitions is 1GB, 1.5GB, 2.5GB respectively, then the total scanning amount of the query is 5GB, then the total cost of this task is: 0.0001 \* 5 = $0.0005.

<span id="c9edd210"></span>
## Subscription (Prepaid)

This scenario only includes **a completely fixed annual subscription model** , and the purchase **instance/exclusive queue** can use this resource form to pay the fee according to the number of resources configured when purchasing the queue. The specific unit price and description are as follows:

<span id="5d239228"></span>
### Serverless Queues

**Case estimate**

The calculation model is as follows ( **Asia Pacific (Johor)**  ):


* Assume that when the user chooses to purchase the annual package, the queue specification of 128 CU is configured and used for 1 month. Then this part of the resources needs to be calculated according to the annual subscription.


**Cost estimate:** 


|**Billing method** |**Cost** |**Explain** |
|---|---|---|
|Subscription |$6400 = 128 CU × $50/CU/month × 1 month |prepaid |


<span id="084ae727"></span>
## Hybrid billing

This scenario also includes **the model of annual subscription and monthly payment according to the amount** . The purchase of **exclusive queues and the opening of elastic resources** can use these two resource forms in a queue. Among them, annual subscription and monthly subscription are prepaid, and elastic payment is postpaid. The specific unit price and description are as follows:

&nbsp;

**Case estimate**

Suppose the computational model is as follows:


* Suppose the user purchases a package year\-month and selects Elastic Resources, and configures a queue with a MIN value of 128CU and a MAX value of 256CU. The resources in the MIN value part need to be calculated according to the package year and month, and the MIN value to the MAX value part (128, 256] is billed according to the actual usage (plus hours).


**Cost estimate:** 


|**Billing method** |**cost** |**explain** |
|---|---|---|
|Subscription |$6400 = 128 CU × $50/CU/month |prepaid |
|Pay\-As\-You\-Go |$ x. Unit price $0.12/CU/hour |postpaid |
|total cost |$6400+x |— |
