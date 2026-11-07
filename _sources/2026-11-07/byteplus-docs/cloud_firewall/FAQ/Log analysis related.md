---
title: "Log analysis related"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Log_analysis_related"
---

<span id="42d41bc7"></span>
## Insufficient log storage space, how to reduce log analysis storage capacity without expansion?


* **Reduce log storage duration**: The default log analysis storage duration is 180 days. If you confirm that the business does not need to retain historical logs for a long time, you can manually modify the log storage duration. For details, see [Set log parameters](https://docs.byteplus.com/en/docs/6516/1171782).

* **Reduce log collection types**: The cloud firewall collects all log types by default. If you confirm that you only need to collect a certain type of log, you can manually modify the types of logs to be collected. For details, see [Set log parameters](https://docs.byteplus.com/en/docs/6516/1171782).


<span id="d97367ae"></span>
## Does the cloud firewall's traffic logs support export to third\-party tools? 

Log analysis provides real\-time data consumption and delivery functions, supporting the consumption of data collected in the log service to third\-party tools through SDK, or delivering to BytePlus TOS and other products for subsequent log processing and big data computation analysis.


|Function |Plan |Note |Related documents |
|---|---|---|---|
|Data consumption |Consume logs through the Kafka protocol |Real\-time consume data from the log topic to third\-party tools or systems through the Kakfa protocol of the stream computing framework. |* [Consume logs via Kafka protocol](https://docs.byteplus.com/en/docs/6470/134625)<br><br>* [Consume logs via Spark Streaming](https://docs.byteplus.com/en/docs/6470/177146)<br><br>* [Consume logs via Flink](https://docs.byteplus.com/en/docs/6470/177209)<br><br>* [Consume logs via ByteHouse](https://docs.byteplus.com/en/docs/6470/169876) |
||Normal consumption |Consume data from the log topic through the ConsumeLogs API provided by the log service. |[Consume logs through ConsumeLogs](https://docs.byteplus.com/en/docs/6470/132354) |
||Consume through the consumption group |Use the multilingual application as the consumption group to consume data from the log service. |[Consume data through the consumption group](https://docs.byteplus.com/en/docs/6470/1152208) |
|Data delivery |Deliver data to TOS |Deliver log data to BytePlus object storage products according to specified delivery rules for long\-term storage and archiving. |[Deliver logs to TOS](https://docs.byteplus.com/en/docs/6470/155599) |
||Deliver logs to Kafka |Deliver log data to the BytePlus message queue Kafka version according to the specified delivery rules for downstream third\-party systems to consume. |[Deliver logs to Kafka](https://docs.byteplus.com/en/docs/6470/1152627) |


For more details, please refer to [Overview of consumption and delivery](https://docs.byteplus.com/en/docs/6470/1144263).

<span id="90db0edf"></span>
### How to download logs?


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview), click on **Log Management** in the left navigation bar.

2. Select Advanced mode at the top right of the page.

3. Retrieve the logs you wish to download by using time range, search criteria, etc., and click the download log button in the top right corner to download the logs.
