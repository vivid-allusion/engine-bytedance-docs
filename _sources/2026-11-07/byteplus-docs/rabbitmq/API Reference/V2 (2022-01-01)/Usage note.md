---
title: "Usage note"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Usage_note"
---

Message Queue for RabbitMQ is a middleware service provided by BytePlus. Message Queue for RabbitMQ is built on a highly available distributed cluster technology. It offers a reliable, scalable, and flexible managed message queue. It is widely used in scenarios such as flash sales, traffic control, and system decoupling.

<span id="8e46f8ab"></span>
## Call description

Message Queue for RabbitMQ provides an Open API that you can call by sending HTTPS requests.

When calling the API, you need to send HTTPS requests to the BytePlus Message Queue for RabbitMQ API server address. Refer to each business interface section and include the correct request parameters in the HTTPS request. The server will return the processing results after receiving the request. Please employ UTF\-8 character set to encode HTTPS requests and responses.

<span id="0539d0ea"></span>
## Usage limits


* The rate limit for each user to call each API is 20 times per second. If the server returns AccountFlowLimitExceeded, it means flow control restrictions have been triggered.

* Each BytePlus account can create up to 5 instances per region in the Message Queue for RabbitMQ version. If you need more instances, please apply to increase the quota in the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=RabbitMQ). For detailed constraints and limits, refer to the [Restriction description](https://docs.byteplus.com/en/docs/rabbitmq/Restriction_description).
