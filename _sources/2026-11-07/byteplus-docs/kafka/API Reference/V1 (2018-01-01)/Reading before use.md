---
title: "Reading before use"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Reading-v1"
---

Message queue Kafka is a message middleware service provided by Byteplus Engine. Based on high\-availability distributed clustering technology, Kafka provides a highly reliable, scalable, and flexible routing managed message queue, which is widely used in scenarios such as seckill, flow control, and system decoupling.

<span id="f5f97408"></span>
## Call instructions

Message queue Kafka version provides OpenAPI, you can call the message queue Kafka version API by sending HTTPS requests.

When calling the API, you need to send an HTTPS request to the server level address of the Byteplus Engine message queue Kafka version API, and refer to the various business interface documents, fill in the correct request parameters in the HTTPS request, and the server level will return the processing result after receiving the request. HTTPS requests and return results are encoded in the UTF\-8 character set.

For detailed interface call instructions, please refer to [Request structure](https://docs.byteplus.com/en/docs/kafka/Request-structure-v1).

<span id="208cbd2f"></span>
## Use restrictions


* Each Byteplus Engine account can create 2 instances under each region of the message queue Kafka version. If you need more instances, please click on Quota Center Apply to increase the quota.

* The flow control limit of each API is different. The flow control limit of the query class API is 100 times/second, and the flow control limit of other APIs is 20 times/second. If the server level returns AccountFlowLimitExceeded, it means that the flow control limit has been triggered.
