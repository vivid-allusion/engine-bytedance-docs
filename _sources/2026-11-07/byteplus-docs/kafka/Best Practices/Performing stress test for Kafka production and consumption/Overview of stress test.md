---
title: "Overview of stress test"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/overview-of-stress-test"
---

This topic describes how to conduct performance testing for Kafka production and consumption using open\-source Kafka tools.

<span id="9de27f3a"></span>
## Testing tools

You can use the open\-source scripts included in the Kafka client for performance testing of Kafka Producer and Consumer. The main metrics are messages sent per second (records/second) and data sent per second (MB/second).

Take open\-source Kafka 2.2.2 toolkit as an example, which can be downloaded from the following link: https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11\-2.2.2.tgz

After downloading and extracting, note the following paths:


* Producer test script: `/bin/kafka-producer-perf-test.sh`

* Consumer test script: `/bin/kafka-consumer-perf-test.sh`

* Producer configuration file: `/config/producer.properties`

* Consumer configuration file: `/config/consumer.properties`


<span id="dd95df77"></span>
## Stress testing methods

Kafka instances can be accessed by default and SASL endpoints. You can choose the appropriate method for your stress test from the following:


* [Using default endpoint for stress testing](https://docs.byteplus.com/docs/kafka/32221)

* [Using SASL_PLAINTEXT endpoint for stress testing](https://docs.byteplus.com/docs/kafka/32220)

* [Using SASL_SSL endpoint for stress testing](https://docs.byteplus.com/docs/kafka/32218)
