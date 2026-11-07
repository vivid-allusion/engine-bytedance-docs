---
title: "Consuming RocketMQ message queues through Function Service"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Consuming_RocketMQ_message_queues_through_Function_Service"
---

The following content introduces the advantages, use scenarios, business cases, and related documents for consuming RocketMQ message queues through FaaS.

<span id=".5LyY5Yq_"></span>
## Advantages

The FaaS is a fully managed and Serverless computing platform that is driven by events. With the RocketMQ trigger provided by the FaaS, developers can easily connect to the RocketMQ Topic to be consumed, without worrying about the details of message consumption, allowing full focus on the business logic of message processing.


* **Low entry barrier**: no language barrier, no need to learn big data frameworks, only focus on the business logic of message processing.

* **Low operation cost**: no need to manage or maintain underlying infrastructure such as servers and provides general governance of MQ consumption.

* **Automatic scaling**: automatic scale\-in/out for function instances based on business traffic to ensure reliable service operation.

* **Low resource cost**: computing resources are billed based on request count and actual execution time, and there is no charge if no execution is performed, further reducing resource costs. Meanwhile, multiple concurrent requests per instance improves resource utilization.


<span id=".5L2_55So5Zy65pmv"></span>
## Use cases

The FaaS is applicable to general large\-scale scenarios that require elastic consumption, mainly including:


* **Real\-time ETL**: use of triggers allows customized processing and storage of upstream data.

* **Offline consumption**: applicable to scenarios with large amounts of data, multiple data sources, and significant traffic variations, considerably reducing costs.

* **Middleware scenario**: maintains and manages numerous consumers without need for resource or scaling management.


<span id=".5Lia5Yqh5qGI5L6L"></span>
## Business case

Wallet deposit service for Douyin red envelope rain needs to handle heavy traffic and surges with low latency and high stability. The FaaS ensures real\-time consumption of red envelope messages from RocketMQ, allowing tens of millions, even hundreds of millions of deposit operations accomplished within a few minutes. With the elastic scaling capability of the FaaS, consumption performance can increase based on real\-time business traffic to ensure time\-sensitive data can be processed concurrently. When the traffic decreases to a low level, the FaaS will automatically scale in to avoid resource waste.

<span id=".5L2_55So5oyH5Y2X"></span>
## User guide


* For details about using the FaaS to realize message consumption from RocketMQ, see [Creating RocketMQ triggers](https://docs.byteplus.com/en/docs/faas/Creating_a_RocketMQ_trigger).

* To quickly learn about the basic usage of the FaaS, see [Quick Start Guide for Beginners](https://docs.byteplus.com/en/docs/faas/FaaS_Quick_Start).
