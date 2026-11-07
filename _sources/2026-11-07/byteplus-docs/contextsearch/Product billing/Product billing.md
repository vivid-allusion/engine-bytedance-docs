---
title: "Product billing"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Productbilling"
---

Contextual search has been officially available for sale since Beijing time May 18, 2026 This topic describes the product billing details for contextual search.

## Billable items

|Billable item |Billing type |Description |
|---|---|---|
|Instance node |Pay\-as\-you\-go |Charges are incurred based on the node type, node specification, billing type, and purchase or usage duration you select when creating the database scenario. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario). |
|model invocation |Pay\-as\-you\-go |Charges are based on the number of tokens consumed when invoking AI model services, with fees collected by Volcano Ark. |
|Serverless service |Pay\-as\-you\-go |Charges are based on the number of tokens consumed using Serverless services. |

## Billable item details

**Instance node**

Instance nodes support two resource types: CPU and GPU. Prices vary for different resource types.

**CPU resource billing**

|Specification |Resource ratio (CPU/Memory) |Region |Pay\-as\-you\-go (USD/hour) |
|---|---|---|---|
|ai.cu.2x |1:2 |Asia Pacific (Johor) |0.05 |
|ai.cu.2x |1:4 ||0.07 |
|ai.cu.2x |1:8 ||0.09 |

**GPU resource billing**

|Specification |GPU model |Region |Pay\-as\-you\-go (USD/hour) |
|---|---|---|---|
|ai.gni3cl.20c\-120gi |GNI3CL (1GNI3CLGPU 20vCPU 120GiB) |Asia Pacific (Johor) |3.39 |

**Model invocation**

Model call fees are charged by Volcano Ark based on the actual input and output token usage. For specific model prices and billing rules, see [ModelArk Pricing](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/1544106).

**Serverless service**

|Billable item |Region |Pay\-as\-you\-go (USD/K tokens) |
|---|---|---|
|AI\-Serverless\-rerank |Asia Pacific (Johor) |0.00012 |
|AI\-Serverless\-embedding ||0.00007 |
