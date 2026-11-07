---
title: "Billing for Edge Functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/billing_edge_functions_en"
---

Edge Functions is a paid feature. This document introduces the billing rules of Edge Functions to help you better estimate and manage your costs.

<span id="billing-method"></span>
## Billing method

Edge Functions uses a post\-paid, **pay\-as\-you\-go** billing model.

<span id="billing-cycle"></span>
## Billing cycle

Bills for the previous month's costs are issued monthly.

<span id="billing-items"></span>
## Billing items

The billing items for Edge Functions include:


|Billing item |Description |
|---|---|
|**Requests** |The number of times a function is triggered by a [trigger](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-concepts#trigger) and successfully executed. |
|**Edge KV write operations** |The number of times a function successfully writes a key\-value pair to Edge KV by calling [KV.set()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI#kv-set). |
|**Edge KV read operations** |The number of times a function successfully reads the value of a key\-value pair from Edge KV by calling [KV.get()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI#kv-get). |
|**Edge KV delete operations** |The number of times a function successfully deletes a key\-value pair from Edge KV by calling [KV.delete()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI#kv-delete). |
|**Edge KV storage** |The monthly average peak usage of data stored at Edge KV. The billing unit price is per GB per month. The system calculates the storage peak on a daily basis and uses the average of the daily peaks as the billing data volume for the month. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Edge Functions does not charge for sub\-requests. A sub\-request is an HTTP or HTTPS request successfully sent by a function. Please note that there is a limit to the number of sub\-requests that a running function can send. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Usage_Limits_Functions">Usage Limits</a>.</div>


<span id="free-tier"></span>
## Free tier

Edge Functions provides a one\-time free tier for each BytePlus account every month. This free tier is automatically reset on the first day of each calendar month.


|Billing item |Monthly free tier |
|---|---|
|**Requests** |2,000,000 |
|**Edge KV write operations** |20,000 |
|**Edge KV read operations** |2,000,000 |
|**Edge KV delete operations** |20,000 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The free tier is only valid for the current month. Unused portions will not be carried over to the next month.</div>


* <div data-tips="true" data-tips-type="tip">There is no free tier for Edge KV Storage.</div>



<span id="pricing"></span>
## Pricing

When your usage exceeds the free tier, the system will start billing for the excess usage.


|Billing item |Unit price |
|---|---|
|**Requests** |$0.3 / million |
|**Edge KV write operations** |$5 / million |
|**Edge KV read operations** |$0.5 / million |
|**Edge KV delete operations** |$5 / million |
|**Edge KV stored data** |$0.5 / GB / month |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For Edge KV write, read, and delete operations, if the number of operations is less than 1 million, it will be billed as 1 million operations.</div>


<span id="billing-example"></span>
## Billing example

<span id="usage"></span>
### Usage

Assume the following usage for the month:


* Function requests: **3,000,000** (exceeds the free allowance by 1,000,000).

* Edge KV write requests: **1,020,000** (exceeds the free allowance by 1,000,000).

* Edge KV delete requests: **15,000** (within the 20,000 free allowance).

* Edge KV read requests: **1,020,000** (within the 2,000,000 free allowance).

* Edge KV storage: Monthly average peak value is **10 GB**.


<span id="costs"></span>
### Costs


* **Function Requests**:

   Exceeded portion: `(3,000,000 - 2,000,000) / 1,000,000 × $0.3 = $0.30`

* **Edge KV Write Requests**:

   Exceeded portion: `(1,020,000 - 20,000) / 1,000,000 × $5 = $5.00`

* **Edge KV Delete Requests**:

   Exceeded portion is 0; cost: `$0.00`

* **Edge KV Read Requests**:

   Exceeded portion is 0; cost: `$0.00`

* **Edge KV Storage**:

   `10 GB × 1 month × $0.5/GB/month = $5.00`


Monthly total cost = $0.30 + $5.00 + $0.00 + $0.00 + $5.00 =  **$10.30**.
