---
title: "Consuming message queue for Kafka through Function Service"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Consuming_message_queue_for_Kafka_through_Function_Service"
---

This article introduces the advantages, use scenarios, business cases, and related document links of consuming message queue for Kafka through Function Service.

<span id=".5LyY5Yq_"></span>
## Advantages

Function Service (FaaS) is an event\-driven, fully managed Serverless computing platform. Through the Kafka Trigger provided by Function Service, the developers can easily integrate with the Kafka Topic to be consumed, without caring for the consumption message details of Function Service, and focus on the business logic of handling messages to the maximum.


* **Low entry cost**: There are no language restrictions and you do not need to learn the big data framework. You only need to focus on the message handling logic of businesses.

* **Low operation and maintenance cost**: You do not need to manage or maintain servers or other underlying infrastructure. Also, Function Service provides general MQ consumption governance capability.

* **Automatic scaling**: Function Service automatically expands and contracts function instances according to business traffic, guaranteeing highly reliable service operation.

* **Low resource cost**: Computing resources are billed according to the number of requests and actual execution duration, and no execution, no charges, thus further reducing resource cost. Meanwhile, FaaS supports multiple concurrent requests per instance to improve resource utilization rate.


<span id=".5L2_55So5Zy65pmv"></span>
## Use scenarios

Function Service is applied in the general large\-scale, elastic consumption scenarios, mainly including:


* **Real\-time** **ETL**: FaaS supports the customized processing and dumping of upstream data through triggers.

* **Offline consumption**: FaaS can be applied in scenarios with a large amount of data, multiple data sources, and enormous gap between peak and trough traffic, and can significantly lower the cost.

* **Middle\-end business**: FaaS maintains and manages a large number of consumers, without managing resources and scaling.


<span id=".5Lia5Yqh5qGI5L6L"></span>
## Business cases


* **TikTok red packet rain wallet transactions**

   The TikTok red packet rain wallet transaction businesses feature large traffic, low latency, and high stability, accompanied by a sudden increase in traffic. After consuming Kafka in real time through Function Service and writing the red packet transactions message in the databank, millions of and billions of users can receive funds in a few minutes. The Function Service features an instant elastic scaling capability, allowing scaling up consumption in real time based on business traffic, and concurrent processing, guaranteeing the timeliness and stability of data processing. During business troughs, Function Service automatically scales down to prevent resource waste.

* **MQ middle\-end business**

   MQ middle\-end business usually demands the processing of hundreds of thousands of message queues, featuring large traffic and multiple upstreams and downstreams. Therefore, it has a high requirement for resource isolation, dynamic scaling, and efficient development and maintenance. Through the Kafka Trigger feature provided by Function Service, this business can quickly connect with and manage massive Kafka consumers, without needing to pay attention to consumer realization. Users only need to use the programming language that they are familiar with to complete message handling logic, and thus they can efficiently consume, process, and deliver messages. Further, based on the serverless automatic scaling capability provided by functions, users do not need to care about the function resource allocation, because function instances can automatically scale up and down according to business traffic, and users only need to make payments according to function execution duration. For scenarios with evident peaks and troughs, the resource cost is lower. Eventually, through OpenAI provided by Function Service, users can quickly and easily build their own business platforms.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca18aad6d70208250aa8fc0ec676b306.jpg) </span>


<span id=".5L2_55So5oyH5Y2X"></span>
## User Guide


* For the information of consuming message queue for Kafka through Function Service, refer to [Creating Kafka Triggers](https://docs.byteplus.com/en/docs/faas/Creating_a_Kafka_trigger).

* To quickly learn about the basic usage process of Function Service, refer to [Getting started](https://docs.byteplus.com/en/docs/faas/FaaS_Quick_Start).
