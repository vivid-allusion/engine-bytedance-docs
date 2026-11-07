---
title: "Signature method"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Signature_method"
---

Message Queue for RabbitMQ uses BytePlus's unified signature method. 

To ensure the requester's identity is valid and the request remains unaltered during transmission, BytePlus's signature method requires the requester to hash the request parameters, encrypt the result, and send it together with the API request to the server. The server calculates the signature of the received request using the same method and compares it with the signature from the requester. If the signature verification fails, the request will be denied.
