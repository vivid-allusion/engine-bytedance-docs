---
title: "[Announcement] Commercialization announcement for EMR Spark on Native engine Bolt"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Commercialization-announcement-for-EMR-Spark-on-Native-engine-Bolt"
---

The Volcengine E\-MapReduce (EMR) Serverless team's self\-developed **Spark on Native engine Bolt** will officially begin commercial billing starting from **October 12, 2026**.

Bolt accelerates SparkSQL jobs through the Native execution engine, effectively improving job execution efficiency, shortening runtime, and reducing overall compute resource consumption in most scenarios. After commercialization, users will pay the corresponding acceleration fee for Bolt based on the actual CUH consumed by their jobs when using Bolt acceleration capabilities.

**1. Limits**


* Only supports **EMR Serverless** mode

* Only applies to **SparkSQL** jobs


**2. Billing rules**

Bolt acceleration fees are billed based on the **actual CUH consumed by SparkSQL jobs**. The fee structure varies depending on the queue type:


|Queue type |Fee structure |Note |
|---|---|---|
|Dedicated queue |Queue fee + Bolt acceleration fee |The actual compute fee for the job is already included in the dedicated queue fee. After enabling Bolt, only the additional acceleration fee needs to be paid. |
|Public queue |Job computing cost + Bolt acceleration cost |After Bolt is enabled, both the job computing cost and Bolt acceleration cost must be paid |


Bolt acceleration can effectively reduce job runtime and CUH consumption, so even with additional acceleration fees, the overall job cost may still decrease.

For existing SparkSQL tasks with Bolt enabled before commercialization takes effect, Bolt acceleration fees will be charged according to the billing rules in this announcement starting from the effective date. To avoid Bolt acceleration fees for existing tasks after commercialization takes effect, disable the Bolt acceleration configuration for relevant tasks before the effective date. Tasks without Bolt enabled are not affected by this commercialization billing. After commercialization takes effect, SparkSQL tasks with Bolt newly enabled will be charged Bolt acceleration fees based on actual job CUH consumption.

The unit price for Bolt acceleration fees is as follows


|Region |Unit price |Unit |
|---|---|---|
|Asia Pacific Southeast (Johor) |0.042463 |USD/CUH |
|Asia Pacific Southeast (Jakarta) |0.036094 |USD/CUH |


If you have any questions about Bolt commercialization billing rules, use cases, or usage methods, please submit a ticket or contact your dedicated technical support at any time.

Thank you for your continued trust and support for Volcengine EMR!
