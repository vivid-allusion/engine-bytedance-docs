---
title: "Signature method"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Signature_method"
---

To ensure the legitimacy of the requester's identity and protect the request from being maliciously tampered with during transmission, the BytePlus signature mechanism requires the requester to compute a hash value of the request parameters, encrypt it, and send it together with the OpenAPI request to the server. The server will perform the same signature calculation on the received request and compare it with the signature provided by the requester. If the signature fails verification, the request will be denied. See [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).
