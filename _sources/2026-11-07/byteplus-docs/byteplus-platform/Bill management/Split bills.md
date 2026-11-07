---
title: "Split bills"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/SplitBills"
---

<span id="feature-overview"></span>
# Feature Overview

Fees for usage of pay\-as\-you\-go products are billed based on split items. For example, traffic fees in CDN are billed by domain, storage fees in TOS are billed by bucket, and bandwidth fees in a shared bandwidth package are billed by EIP. These domains, buckets, and EIPs are called split items of the corresponding product.

Split bills are applicable to such pay\-as\-you\-go products and also other products. A split bill contains the specific usage, usage proportion, and fees of each split item. These details can be used as a reference for bill splitting within enterprises.

Note: If you have multiple accounts that have a financial custody relationship, please log in to each account to activate and view split bills respectively.

<span id="X55X8IXe"></span>
# Operation Procedure

1. Select [Bill - split bills](https://console.byteplus.com/finance/bill/split-bill) and activate the split bills service. Note: After activation, for each new bill, a split bill is generated accordingly. Data in split bills is subject to a delay no longer than two days. Split bills data will not be generated for bills generated before this service is activated.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260527101417-955010007221.png) </span>

2. After the service is activated, you can view split bills details on the Split bills page. Some key fields are as follows:


* Billing cycle: the accounting period to which this split bill is allocated.

* Payer: the user account that is due to pay the bill.

* Owner: the user account that actually uses the services billed.

* Product: the name of a cloud product.

* Instance ID: the ID and name of an instance.

* Billing unit: the billing unit of an instance or a billable item, such as traffic, bandwidth, and storage.

* Split item ID: the ID of a split item, such as a domain in CDN or a bucket in TOS.

* Split item name: the name of a split item.

* Usage: the usage amount of a split item. The monthly total is displayed when data is aggregated by accounting period.

   * Note: The method for collecting usage statistics of split items is consistent with the method for collecting statistics of total usage. For example, if CDN uses the monthly 95th percentile billing method to meter bandwidth usage, then this method is also used to collect bandwidth usage statistics of each split item (namely, domain) to serve as a reference for bill splitting.

* Percentage of split item usage: the proportion of the usage amount of a split item to total usage. This field is not displayed when data is aggregated by accounting period.

* For descriptions of other fields, see [Bill Details](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).


3. View and export split bills data on the Split bills page.


* Export: Click the export icon. In the Export bill CSV pop\-up window, set the conditions for exporting data and click OK.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260527101816-1336305916951.png) </span>

4. View split bills by Apikey.


* Each API Key is assigned a unique Resource ID by Model Ark to support Split bills and usage statistics;Log in to the Ark Console, then retrieve the Resource ID on the [API Key Management](https://console.byteplus.com/ark/region:ark+ap-southeast-1/apiKey?apikey=%7B%7D) page.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260527111058-1775981655031.png) </span>

* Go to the [Split Billing](https://console.byteplus.com/finance/bill/split-bill) page, click **Set Split Dimensions**, and select **apikey_id**.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260527111439-1559857524966.png) </span>

* When apikey_id is configured as the split dimension, the Split Item ID displayed in split bills refers to the Resource ID of the Ark API Key.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260527111707-1618838742697.png) </span>


&nbsp;

&nbsp;
