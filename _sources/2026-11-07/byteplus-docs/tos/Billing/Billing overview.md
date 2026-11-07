---
title: "Billing overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-billing-overview"
---

This topic describes TOS billing and billable items.

<span id="a53f66ad"></span>
## Overview

All TOS cost components, or billable items are billed separately. For example, storing files incurs a storage fee. File reads and writes are charged based on the number of requests. Accessing TOS files from the internet also incurs a data transfer fee.

<span id="95856760"></span>
## Billing cycle

Unless otherwise specified, TOS generates a bill by usage per hour for all billable items. Some billable items, such as image processing, are charged monthly. Refer to the corresponding billing documentation for details.

<span id="19f2dac3"></span>
## Billing method

TOS supports **Pay\-as\-you\-go**. It is a postpaid billing method, which means you use the service first and then pay for it. Specifically, bills are calculated by multiplying usage by the unit price. Then, you can pay the bill. For more information, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/tos/docs-billing-by-volume).

<span id="vsZrtQS4"></span>
## Cost components


|**Type** |**Description** |
|---|---|
|[Storage](https://docs.byteplus.com/en/docs/tos/docs-storage-fee) |Storing files in TOS incurs the storage fee. |
|[Data transfer](https://docs.byteplus.com/en/docs/tos/docs-traffic-fee) |Uploading files to TOS or accessing files in TOS incurs the traffic fee. |
|[Requests](https://docs.byteplus.com/en/docs/tos/docs-request-fee) |You can access TOS through the console, SDKs, APIs, or clients. Regardless of the method used, TOS APIs are called to perform operations, which incurs request costs. |
|[Data retrievals](https://docs.byteplus.com/en/docs/tos/docs-data-retrieval-fee) |Accessing files in Infrequent Access Storage, Flashback Archive, or another storage type incurs the data retrieval fee. |
|[Data processing](https://docs.byteplus.com/en/docs/tos/docs-data-processing-fee) |Using features such as image processing and advanced image compression incurs the data processing fee. |
|[Storage of temporary copies](https://docs.byteplus.com/en/docs/tos/docs-temporary-storage-fee) |After a file is restored from Archive Storage or Cold Archive, TOS will generate a temporary copy in Standard Storage for your access. The copy will be deleted automatically after the validity period you specify. Within the validity period, the copy incurs the temporary storage fee. |
|[Storage analytics](https://docs.byteplus.com/en/docs/tos/Storage-analytics) |You pay to use Storage Lens with advanced metrics. |
|[TOS accelerator](https://docs.byteplus.com/en/docs/tos/TOS_Accelerator_fee) |You pay for using TOS accelerator. |


<span id="Doe2jDso"></span>
## Pricing details

For pricing information on TOS billable items, see [TOS pricing](https://www.byteplus.com/en/pricing?product=TOS&tab=1).
