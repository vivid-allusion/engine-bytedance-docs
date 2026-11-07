---
title: "Bolt acceleration engine pricing details"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Billing_for_Bolt"
---

Bolt accelerates SparkSQL jobs through the Native execution engine, effectively improving job execution efficiency, shortening runtime, and reducing overall compute resource consumption in most scenarios. When using Bolt acceleration, users pay the corresponding acceleration fee based on the actual CUH consumed by the job.

<span id="ef4b64f2"></span>
# **Limits**


* Only supports **EMR Serverless** mode

* Only applies to **SparkSQL** jobs


<span id="6152a1e4"></span>
# **Billing rules**

Bolt acceleration fees are charged based on **the actual CUH consumed by SparkSQL jobs**. The fee structure varies by queue type:


|Queue type |Fee structure |Note |
|---|---|---|
|Dedicated queue |Queue fee + Bolt acceleration fee |The actual compute fee for the job is already included in the dedicated queue fee. After enabling Bolt, only the additional acceleration fee needs to be paid. |
|Shared queue |Job compute fee + Bolt acceleration fee |After enabling Bolt, both the job compute fee and Bolt acceleration fee must be paid. |


Bolt acceleration can significantly reduce job runtime and CUH consumption, so even with additional acceleration fees, the overall job cost will still decrease.

The unit price for Bolt acceleration fees is as follows:


|Region |Unit price |Unit |
|---|---|---|
|Asia Pacific Southeast (Johor) |0.042463 |USD/CUH |
|Asia Pacific Southeast (Jakarta) |0.036094 |USD/CUH |
