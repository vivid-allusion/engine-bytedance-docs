---
title: "Signature method"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/signature-method-v2"
---

In order to ensure the legitimacy of the requestor's identity and the request is not maliciously tampered with during transmission, the Byteplus Engine signature mechanism requires the requestor to calculate the hash value of the request parameters. After encryption, it is sent to the server together with the API request. The server will use the same mechanism to calculate the signature of the received request and compare it with the signature sent by the requestor. If the signature fails to be verified, the request will be rejected.

For more information, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
