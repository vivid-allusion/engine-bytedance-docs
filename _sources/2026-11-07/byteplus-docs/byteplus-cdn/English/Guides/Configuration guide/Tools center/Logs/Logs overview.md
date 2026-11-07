---
title: "Logs  overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/logs-overview_en-us"
---

CDN request logs provide detailed information about user access, which is crucial for data analysis and issue troubleshooting. BytePlus offers three methods for obtaining these logs: Log Download, Log Batch Delivery, and Log Streaming. This document compares their differences in timeliness, cost, and use cases to help you select the most suitable method for your business needs.


| |**Log Download** |**Log Batch Delivery** |**Log Streaming** |
|---|---|---|---|
|**Log Timeliness** |* After collection, logs are grouped into a log package. Within approximately 3 hours, the log package is available for download.<br><br>* You can download request logs from the past 62 days. |Logs are delivered by CDN within 5 minutes after collection. | |
|**Log Delay** |Maximum 24 hours |||
|**Delayed Log Processing Method** |Appended to the generated log package. |Appended to the delivered log package. |Delayed logs are delivered separately. |
|**Use Cases** |* Data analysis (low requirements for log timeliness)<br><br>* Log storage ||* Metric monitoring<br><br>* Data analysis (high requirements for log timeliness)<br><br>* Log storage |
|**Cost** |Free |Billed based on the number of log entries delivered. See [Billing Details](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-pricing#billing-details-pay-as-you-go). ||
