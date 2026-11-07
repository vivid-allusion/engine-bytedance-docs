---
title: "Resource Pool Overview"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Resource_Pool_Overview"
---

In the Flink stream computing project, computational resources are managed through resource pools, and a resource pool must be created before starting development tasks. This article introduces concepts related to resources on the Flink console to help you understand resource types and the purposes of resource pools.

<span id="1632b569"></span>
## Glossary Explanation


|**Concepts** |**Description** |
|---|---|
|Resource Types |General Resources: Currently supports the creation of resource pools based on VCI type resources. |
|Resource Models |VCI Mode: A serverless and containerized elastic container service that does not require attention to underlying cloud servers or other infrastructure. |
|Billing Type |Different resource pools support different billing methods.<br><br><br>* Pay\-as\-you\-go: Supports payment based on the actual duration of CU resources used by Flink. For more details, refer to: [Pay-As-You-Go](https://docs.byteplus.com/docs/flink/Pay-As-You-Go)<br><br>* Subscription: Supports the pre\-purchase of CU resources for Flink operations, and the reasonable planning and allocation of CPU and memory resources. For more details, refer to: [Annual and Monthly Subscription](https://docs.byteplus.com/docs/flink/Annual_and_Monthly_Subscription) |
|Session Cluster |Session Cluster is a cluster that is pre\-started and continuously runs, used solely for debugging Flink SQL jobs. |
