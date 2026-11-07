---
title: "Reading before use"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/reading-V2"
---

Message queue Kafka is a message middleware service provided by Byteplus Engine. Based on high\-availability distributed clustering technology, Kafka provides a highly reliable, scalable, and flexible routing managed message queue, which is widely used in scenarios such as seckill, flow control, and system decoupling.

<span id="f8960e5b"></span>
## Call instructions

Message queue Kafka Edition provides a new version of V2 OpenAPI, you can call the message queue Kafka Edition V2 API by sending an HTTPS request.

When calling the V2 API, you need to send an HTTPS request to the server level address of the Byteplus Engine message queue Kafka version API, and refer to the various business interface documents, fill in the correct request parameters in the HTTPS request, and the server level will return the processing result after receiving the request. HTTPS requests and return results are encoded using the UTF\-8 character set.

For detailed interface call instructions, please refer to [Request structure](https://docs.byteplus.com/en/docs/kafka/request-structure-v2).

<span id="6a37998e"></span>
## Use restrictions


* Each Byteplus Engine account can create 5 instances under each region of the message queue Kafka version. If you need more instances, please click on Quota Center Apply to increase the quota.

* In the V2 version, except for the following APIs, the flow control limit of the rest of the APIs is 20 times/second. If the server level returns `AccountFlowLimitExceeded`, it means that the flow control limit has been triggered.

   * DescribeInstanceDetail: 10 times/second

   * DescribeRegions, DescribeTagsByResource: 50 times/second

   * DescribeAvailabilityZones: 100 times/second
