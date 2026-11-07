---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/kafka_faqs"
---

<span id="q1：timeoutexception"></span>
## Q1：TimeoutException

This error indicates a timeout, which is commonly caused by network connectivity issues. You can use the `telnet` command to test network connectivity. The specific command is as follows:

```shell
telnet {Kafka Broker 地址} 9092
```


If connectivity cannot be established, check the network connectivity between the environment where the Kafka Client is located and the EMR Kafka cluster. For example, verify whether the Client and Broker are in the same VPC (if they are not in the same VPC, check whether mechanisms such as binding a public IP to the Broker have been used to establish connectivity between the Client and Broker), and whether port 9092 is open to the Client in the Broker ECS security group rules configuration.

If network connectivity is not an issue, review the logs on the Kafka Broker machine to determine whether the Kafka process is running normally and whether any errors are reported.

<span id="q2：leader-is-not-available"></span>
## Q2：Leader is not available

This error commonly occurs during Topic creation or service upgrades. If the error persists, it may indicate that the Topic has not been created or there is a server\-side issue. You can use the kafka\-topics.sh script to check the Topic status, and review the logs on the Kafka Broker machine to determine whether the Kafka process is running normally and whether any errors are reported.

<span id="q3：leader-is-not-elected"></span>
## Q3：Leader is not elected

This error may briefly occur during Topic creation and initialization. If the error persists, it may be because the Topic has not been created. You can use the kafka\-topics.sh script to check the Topic status, and review the logs on the Kafka Broker machine to determine whether the Kafka process is running normally and whether any errors are reported.

<span id="q4：disconnectedexception"></span>
## Q4：DisconnectedException

This error is commonly caused by network issues resulting in a timeout or a long\-term idle connection, leading the server to disconnect. Refer to the troubleshooting methods for TimeoutException above, or try reconnecting to Kafka.
