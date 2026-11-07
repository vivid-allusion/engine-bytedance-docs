---
title: "Overview of shipping logs to TOS"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Ship_logs_to_tos_overview1"
---

TLS supports periodically shipping collected server\-side log data to TOS for long\-term storage. This topic introduces the basic concepts and billing information for shipping logs to TOS.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Features overview

BytePlus TOS is a highly reliable and available distributed cloud storage service, offering massive storage capacity, strong security, low cost, ease of use, high reliability, and high availability. TLS supports shipping logs to TOS. After enabling this feature, TLS periodically processes, packages and ships log data to TOS buckets for storage. This solution is ideal for massive data long\-term storage scenarios, offering low prices and high cost\-effectiveness. Additionally, after log data is shipped to TOS, it can be consumed through offline computing or integration with other systems.

When shipping logs, you can configure the following shipping formats.


|Data shipping formats |Description |Related documentation |
|---|---|---|
|JSON format |After the data is shipped to TOS, it is saved in JSON format. As a common data format, JSON is suitable for various structured data scenarios. |[ ](https://docs.byteplus.com/docs/tls/ship_log_in_json_format)[Ship logs in JSON format](https://docs.byteplus.com/docs/tls/ship_log_in_json_format) |
|JSONL format |After the data is shipped to TOS, it is saved in JSONL format. The configuration method is the same as that for JSON format. |[ ](https://docs.byteplus.com/docs/tls/ship_log_in_json_format)[Ship logs in JSON format](https://docs.byteplus.com/docs/tls/ship_log_in_json_format) |
|CSV format |After the data is shipped to TOS, it is saved in CSV format. Fields in CSV files are separated by the specified separator. |[ ](https://docs.byteplus.com/docs/tls/ship_log_in_json_format)[Ship logs in CSV format](https://docs.byteplus.com/docs/tls/ship_log_in_csv_format) |
|Parquet format |After the data is shipped to TOS, it is saved in Parquet format.<br><br><br>* Data scanning performance is better than CSV, JSON, and JSONL, making it suitable for data analysis scenarios.<br><br>* Shipping costs are higher than CSV, JSON, and JSONL. For more details, see [Billing items based on pay-by-feature mode](https://docs.byteplus.com/docs/tls/Billing_items_based_on_pay-by-feature_mode). |[Ship logs in Parquet format](https://docs.byteplus.com/docs/tls/Ship_data_in_Parquet_format) |


&nbsp;

In addition, TLS provides service logs with the log shipping feature. Using this, you can  view the progress and status of shipping tasks. For more details, see [Service log overview](https://docs.byteplus.com/docs/tls/service_logs_overview).

<span id=".6LS555So6K-05piO"></span>
## Billing description

If shipping logs to TOS, fees involve the costs for TLS and data storage costs for TOS.


* Log shipping costs are based on the amount of original logs delivered in JSON, JSONL, CSV, and Parquet formats. For details, see TLS [Billing items based on pay-by-feature mode](https://docs.byteplus.com/docs/tls/Billing_items_based_on_pay-by-feature_mode).

* After log data is shipped to TOS, data storage fees are generated. TOS data storage costs depend on storage usage and bucket type.

   * If data compression is enabled, charges are based on the size of the compressed files.

   * For price details of different bucket types, see [Billing overview](https://docs.byteplus.com/en/docs/tos/docs-billing-overview) in TOS.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits


|<div style="text-align: center"><br>Limitations</div><br> ||Description |
|---|---|---|
|<div style="text-align: center"><br>Account</div><br> ||To deliver logs across accounts, cross\-account delivery permissions must be configured. |
|<div style="text-align: center"><br>Region</div><br> ||Cross\-region log delivery is not supported, that is, the log topic and the TOS bucket should be located in the same region. |
|<div style="text-align: center"><br>Field</div><br> ||When delivering logs, the JSON format by default delivers all fields, including metadata fields such as `__source__`, while the CSV format allows you to configure the list of fields to be delivered. |
|<div style="text-align: center"><br>Resource quotas</div><br> |Number of delivery configurations |Each log topic can have up to 10 TOS delivery configurations. |
||Query delivery tasks |You can only query delivery tasks triggered within the past 3 days. |
||Delivery intervals |The delivery time interval can be set to 60 to 900 seconds. |
||Size of delivered data |Delivered data packets must be between 5 and 256 MiB in size. |


&nbsp;

&nbsp;
