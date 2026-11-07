---
title: "Consumer processor overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Consumer_processor_overview"
---

TLS supports regular real\-time data consumption and rule\-based data consumption processed through the consumer processor. This topic describes the features and usage limitations of the TLS consumer processor.

## Billing notes

We will release billing notes in the upcoming announcement.

## Features overview

### Rule\-based data consumption

The TLS data consumer processor is a powerful tool that pre\-processes and cleans semi\-structured log data on the server side using data transformation syntax. For example, before consuming log data, you can do the following to log data: row filtering, column trimming, regex extraction, and JSON field extraction, etc. This is ideal for scenarios in stream and real\-time computing where data preprocessing is required.

You can create a consumer processor directly in the TLS console and write processing rules using SQL\-like DSL (data processing language). With the processors and rules, you can use the following features such as string masking, encrypting fields, renaming fields, conditional judgment, flow control, and structured handling of JSON fields.

* Use DSL to define data processing rules. For details, see [Data transformation overview](https://docs.byteplus.com/docs/tls/data_transformation_overview).

* Supported data processing functions. For details, see [Functions overview](https://docs.byteplus.com/docs/tls/overview_of_functions).

### Common data consumption

TLS offers the following common data consumption methods. The ConsumeLogs API supports rule\-based data consumption through consumer processors.

|Data consumption types |Reference |
|---|---|
|Consume via Kafka protocol |* [Consume logs via Kafka protocol](https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs)<br><br>* [Consume logs with Spark Streaming](https://docs.byteplus.com/en/docs/tls/use_spark_streaming_to_consume_logs)<br><br>* [Consume logs with Flink](https://docs.byteplus.com/en/docs/tls/use_flink_to_consume_logs)<br><br>* [Consume logs with ByteHouse](https://docs.byteplus.com/en/docs/tls/use_bytehouse_to_consume_logs) |
|Consume with ConsumeLogs API |* [Consume logs using ConsumeLogs](https://docs.byteplus.com/en/docs/tls/use_consumelogs_to_consume_logs) |
|Consume with consumer group |* [Consume data via consumer group](https://docs.byteplus.com/en/docs/tls/using_consumer_groups_to_consume_logs) |

## Features

Data write processors, consumer processors, and data transformation tasks all support real\-time, lightweight log data cleansing, filtering, content masking, and data conversion and data enrichment capability. The main differences are compared as follows:

|Features comparison |Write processor |Consumer processor |Data transformation task |
|---|---|---|---|
|Processing stage |Data before writing to TLS |Data collected in TLS |Data collected in TLS |
|Applicability |* Exists in the project and applies to log topics within the project.<br><br>* Cross\-region, cross\-account, and cross\-project operations are not supported. |* Exists in the project and applies to log topics within the project.<br><br>* Cross\-region, cross\-account, and cross\-project operations are not supported. |* An independent processing task that applies to the selected source log topic and target log topic<br><br>* Supports cross\-region, cross\-account, and cross\-project usage. |
|Billing notes |Currently free of charge. The billing schedule will be announced later. |Currently free of charge. The billing schedule will be announced later. |Data transformation fees and cross\-region transmission costs. |
|Processing rules |You can use built\-in functions provided by TLS DSL to write processing rules.<br><br>The following functions are not supported: e_output, e_auto_output, and res_rds_mysql. |You can use built\-in functions provided by TLS DSL to write processing rules. |You can use built\-in functions provided by TLS DSL to write processing rules. |

## Limits

|**Items** |**Specifications** |
|---|---|
|Number of consumer processors<br><br> |* You can create up to 100 consumer processors in each project.<br><br>* For quota adjustments, see [Apply for resource quota](https://docs.byteplus.com/docs/tls/Apply_for_resource_quota). |
|DSL limitations |* The length of each DSL can not exceed 4,000 characters.<br><br>* Supports only row\-level processing commands. Operations like aggregation and logic judgments are not supported. |
|Effective time |Becomes effective within 1 minute after creating or editing a consumption processor. |
|DSL rules and performance impact |For details, see [Data transformation overview](https://docs.byteplus.com/docs/tls/data_transformation_overview).<br><br>> **Notice**<br><br><br>> If there are DSL syntax errors or missing source data fields, data obtained may be incomplete or fail.<br> |
