---
title: "Overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ship_logs_to_kafka_overview"
---

Torch Log Service (TLS) can ship log data collected to the server to BytePlus Message Queue for Kafka. This way, various types of client applications can consume the log data. This topic describes the terms and billing rules involved when you ship logs to Kafka.

<span id="背景信息"></span>
## Background

BytePlus Message Queue for Kafka is a distributed messaging middleware service built on Apache Kafka. TLS allows you to ship logs to Kafka, which is applicable to scenarios such as big data consumption and real\-time stream computing. If this feature is enabled, TLS ships log data in the specified topic to Message Queue for Kafka in the specified format. This feature allows you to ship historical log data. All log data retained can be shipped to Kafka instances.

In addition, TLS supports the service log feature for data shipping, which allows you to view information such as the progress and status of a shipping task. For more information, refer to [Service log fields](https://docs.byteplus.com/docs/tls/service_log_fields).

<span id="限制说明"></span>
## Limits


* Log data cannot be shipped across Regions. The topic and Kafka instance must be in the same Region.

* Log data cannot be shipped across BytePlus accounts. The topic and Kafka instance must be in the same BytePlus account.

* Up to 10 Kafka shipping configurations can be created for a topic.


<span id="费用说明"></span>
## Cost information

Shipping logs to Kafka incurs data shipping fees from TLS, fees for the Kafka instance specification, and storage fees.

The data shipping fees are calculated based on the volume of the shipped raw logs.
