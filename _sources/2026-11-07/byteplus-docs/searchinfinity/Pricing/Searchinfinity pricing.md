---
title: "Searchinfinity pricing"
product: "Searchinfinity"
product_code: "searchinfinity"
source: "https://docs.byteplus.com/en/docs/searchinfinity/Searchinfinity_pricing"
---

## **Instruction**

Searchinfinity uses credits as the standard unit for usage deductions. Each service is priced separately, and actual usage is converted into credit consumption according to the applicable credit deduction rate.

 **• Service level: ** Each service, including Web Search and Fetch, has its own pricing and credit deduction rate.

 **• API key level: ** An API key is the smallest accumulation unit used by the system for whole\-credit deductions. Credit consumption is accumulated separately for each API key. Whenever the accumulated consumption reaches 1 credit, the system deducts 1 credit from the account. Any remainder below 1 credit continues to accumulate under that API key until it reaches 1 credit and can be deducted.

 **• Account level: ** Deducted credits across multiple services and API keys under the same account are aggregated and charged to that account.

## **Pricing Details**

1. Credit Pricing

| **Billing Method** | **Payment Method** | **Price** |**Description** | **Refund Policy** | **Service Suspension Time (Overdue)**  | **Data Recovery Time (Overdue)**  |**Service Suspension Time **  |**Resource Reclamation Time **  |
|---|---|---|---|---|---|---|---|---|
|Pay\-as\-you\-go (by usage) | Postpaid |$0.006/credit |Usage\-based deduction (postpaid): the system converts each service's actual usage into the corresponding credit consumption and charges the account accordingly. | No refunds<br><br> | 24 hours | 168 hours |\- |\- |

2. Credit conversation breakdown

| ** Service** | ** Price** |**Credit Deduction Rate** |**Description** |
|---|---|---|---|
|Web search\-Flux |$0.006/request |1 credit per 1 request |Each request consumes 1 credit, and 1 credit is deducted. |
|Web search\-Omnira |$0.003/request |1 credit per 2 request |Each request consumes 1/2 credit, and 1 credit is deducted. |
|Fetch |$0.001/request |1 credit per 6 request |Each request consumes 1/6 of a credit. Once 6 requests have accumulated, the system deducts 1 credit. |

3.  Special Note

Searchinfinity has fully transitioned to credit\-based billing. If your account has not yet been migrated, charges will continue to follow the previous billing method until you reactivate credit\-based billing

| **Service Configuration** | **Billing Method** | **Payment Method** | **Price** | **Refund Policy** | **Service Suspension Time (Overdue)**  | **Data Recovery Time (Overdue)**  |**Service Suspension Time **  |**Resource Reclamation Time **  |
|---|---|---|---|---|---|---|---|---|
|Searchinfinity web search |Pay\-as\-you\-go (by usage) | Postpaid |$0.006/request | No refunds | 24 hours | 168 hours |\- |\- |
|Searchinfinity fetch |Pay\-as\-you\-go (by usage) | Postpaid |$0.001/request | No refunds | 24 hours | 168 hours |\- |\- |

4. Usage & Billing

You can view the number of SearchInfinity API calls and detailed usage data in the SearchInfinity API Console. Charges incurred by this service under your account can be viewed in the BytePlus Billing Center under Billing Details.

## **Taxes and Invoices**

Please refer to [Tax rate reference](https://docs.byteplus.com/en/docs/byteplus-platform/docs-tax-rate-reference) and [Managing invoices](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-invoices).
