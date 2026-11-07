---
title: "Data consumption and shipping overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Ship_logs_to_tos_overview"
---

Torch Log Service (TLS) offers real\-time log consumption and log shipping features. Log data collected to TLS can be consumed in third\-party tools or systems through SDKs, or shipped to other products such as Torch Object Storage (TOS) for further log processing and big data computing and analysis.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

TLS offers real\-time log consumption and log shipping features for real\-time big data computing, offline analysis, and long\-term storage and archiving.


* Log consumption means that applications or systems such as third\-party tools and stream computing frameworks consume data in topics in real time using methods such as TLS SDKs. The log consumption feature supports reading data in TLS in the order logs are written. TLS can serve as a data pipeline for data transfer to connect to downstream consumption systems.

* Log shipping means that data collected by TLS is shipped to other products such as TOS to store infrequently accessed data for long, connect to other systems for consumption, and analyze data.


Comparison of the log consumption and log shipping features:


|**Item** |**Consumption** |**Shipping** |
|---|---|---|
|Use Scenario |Real\-time computing, and data analysis |Long\-term data storage and offline analysis |
|Use Method |Automatic code implementation |Wizard configurations in the console |
|Data real\-timeliness |Real\-time |Offline |
|Format |Logs |Raw log, JSON, and CSV |
|Data compression format |Uncompressed, Snappy, gzip, and lz4 |Uncompressed, Snappy, gzip, and lz4 |
|Solution |Normal consumption, using consumer groups for consumption, and using the Kafka protocol for consumption |TOS and Kafka |
|Use scenarios |* Stream computing. Log data is consumed in downstream stream computing systems in real time.<br><br>* Data repository or offline computing. Log data is consumed in downstream big data components or data repositories. |* Data archiving. For example, log data is shipped to IA storage for audit compliance or archiving.<br><br>* Stream computing. Log data is consumed in downstream stream computing systems in real time. |


<span id=".5raI6LS55LiO5oqV6YCS5pa55qGI"></span>
## Consumption and shipping solutions


|Feature |Solution |Description |Related documents |
|---|---|---|---|
|Data consumption |Use the Kafka protocol to consume logs |Use the Kafka protocol to consume log data from topics in third\-party tools or systems in real time. |* [Use Flink to consume logs](https://docs.byteplus.com/docs/tls/use_flink_to_consume_logs)<br><br>* [Use ByteHouse to consume log](https://docs.byteplus.com/docs/tls/use_bytehouse_to_consume_logs)<br><br>* [Use Spark Streaming to consume logs](https://docs.byteplus.com/docs/tls/use_spark_streaming_to_consume_logs)<br><br>* [Use the Kafka protocol to consume logs](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs) |
||Normal Consumption |Use the ConsumeLogs API to consume log data from topics. |[Use ConsumeLogs to consume logs](https://docs.byteplus.com/docs/tls/use_consumelogs_to_consume_logs) |
||Use consumer groups to consume logs |Use multi\-language applications as consumer groups to consume the data from topics. |[Use consumer groups to consume logs](https://docs.byteplus.com/docs/tls/using_consumer_groups_to_consume_logs) |
|Data shipping |Ship data to TOS |Ship log data to BytePlus TOS based on the specified shipping rule for long\-term storage and archiving. |* [Ship log data in JSON format](https://docs.byteplus.com/docs/tls/ship_log_in_json_format)<br><br>* [Ship log data in CSV format](https://docs.byteplus.com/docs/tls/ship_log_in_csv_format) |
||Ship logs to Kafka |Ship log data to Message Queue for Kafka based on the specified shipping rule for consumption in downstream third\-party systems. |[Ship logs to Message Queue for Kafka](https://docs.byteplus.com/docs/tls/ship_logs_to_message_queue_for_kafka) |


<span id=".6LS555So6K-05piO"></span>
## Cost information

The billable items involved in the log consumption and log shipping features are described below. For more information, please refer to [Billable items](https://docs.byteplus.com/docs/tls/billable_items).


* The log consumption feature itself does not incur service fees. However, if you use a public endpoint of TLS to read log data, the read traffic over the internet is generated. If you call the data read API of TLS, you are charged for the number of requests.

* The log shipping feature incurs the traffic fees of data shipping based on the volume of data shipped to TOS.
