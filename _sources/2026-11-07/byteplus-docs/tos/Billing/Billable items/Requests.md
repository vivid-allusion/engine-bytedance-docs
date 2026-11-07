---
title: "Requests"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-request-fee"
---

You can use BytePlus TOS through the console, SDKs, APIs, or clients. No matter which method you use, TOS APIs are called for performing operations, which incurs the request fee.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This topic describes only details about billable items. For more information on pricing, see <a href="https://www.byteplus.com/en/pricing?product=TOS&tab=1">TOS pricing</a>.</div>


* <div data-tips="true" data-tips-type="tip">Requests that fail are not counted toward request quotas or charged as billable requests. Examples of failed requests include those that return 4xx or 5xx status codes.</div>



TOS offers a variety of storage types. The following table lists the billing mode for each storage type.


|**Billable Item** ||**Description** |Formula |
|---|---|---|---|
|Standard Storage \- Read/Write requests ||You are charged based on the number of API requests. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
|Infrequent Access Storage \- Read/Write requests ||You are charged based on the number of API requests. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
|Intelligent Tiering Storage |Intelligent Tiering Storage \- Storage requests |You are charged based on the number of API requests. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
||Intelligent Tiering Storage \- File monitoring |You are charged based on the number of API requests.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Files smaller than 64 KiB are monitored for free.</div><br> |**Pay\-as\-you\-go**: Hourly file monitoring cost = Number of files per hour × Unit price |
|Flashback Archive \- Read/Write requests ||You are charged based on the number of API requests. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
|Archive \- Read/Write requests ||You are charged based on the number of API requests. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
|Cold Archive |Read/Write requests |You are charged based on the number of API requests. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
||Retrieval requests |You need to restore files in Cold Archive before reading them, which incurs retrieval request costs. The unit price per 10,000 requests varies depending on the restoration time. Shorter restoration times result in higher unit prices. Restoration options are as follows:<br><br><br>* Quick: 1–5 minutes<br><br>* Standard: 2–5 hours<br><br>* Batch: 5–12 hours |**Pay\-as\-you\-go**: Hourly request cost = Number of retrieval requests per hour × Unit price per 10,000 requests ÷ 10,000 |
|Deep Cold Archive |Read/Write requests |You are charged by the number of requests for calling APIs. |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
||Retrieval requests |You need to restore files in Deep Cold Archive before reading them, which incurs retrieval request costs. The unit price per 10,000 requests varies depending on the restoration time. Shorter restoration times result in higher unit prices. Restoration options are as follows:<br><br><br>* Standard: Within 12 hours<br><br>* Batch: Within 48 hours |**Pay\-as\-you\-go**: Hourly request cost = Number of requests per hour × Unit price per 10,000 requests ÷ 10,000 |
