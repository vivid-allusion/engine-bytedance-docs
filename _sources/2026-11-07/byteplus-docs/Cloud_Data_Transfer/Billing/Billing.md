---
title: "Billing"
product: "Cloud Data Transfer"
product_code: "Cloud_Data_Transfer"
source: "https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/Billing_overview"
---

## Metering methods

Cloud Data Transfer (CDT) provides unified billing services for Pay\-as\-you\-go cloud products. Pay\-as\-you\-go​ is a postpaid billing model where you are billed after resource usage. You do not need to purchase resources in advance and can provision or release resources on\-demand as needed.

* Supports tiered cumulative pricing for public network traffic.

* Supports pay\-by\-data\-transfer for cross\-region traffic (tiered cumulative pricing is not supported).

* Provides billing and invoicing features only. Actions such as product unsubscription, upgrade/downgrade, and billing conversion must be performed in the respective cloud product's console.

## Billing method overview

|Traffic type |Billing method |Metering method |**Supported products** |**Billing cycle** |
|---|---|---|---|---|
|Public network traffic |Pay\-as\-you\-go |Billed by outbound traffic |Elastic IP Address |Both the billing cycle and the settlement cycle are on an hourly basis.<br><br>On the hour (UTC+8), the platform settles fees, issues bills and deducts corresponding payments from your account balance. For details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details). |
||Pay\-as\-you\-go |Billed by main traffic |Bandwidth Package ||
|Cross\-region traffic |Pay\-as\-you\-go |Billed by outbound traffic |Transit Router |Both the billing cycle and the settlement cycle are on an hourly basis.<br><br>On the hour (UTC+8), the platform settles fees, issues bills and deducts corresponding payments from your account balance. For details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details). |

## Billing documentation

You can understand all aspects of CDT's pay\-as\-you\-go billing by seeing the documents listed in the table below.

|Documentation |Description |
|---|---|
|[Public Network Traffic billing](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/Public_Network_Traffic_billing) |Describes billing details for cloud products with Public Network​ traffic type. |
|[Cross-Region Traffic billing](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/Cross-Region_Traffic_billing) |Describes billing details for cloud products with Cross\-Region traffic type. |

##
