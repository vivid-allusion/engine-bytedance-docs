---
title: "Signature method"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Signature-method"
---

To ensure that the identity of the requester is valid and the request is not tampered with during transmission, the BytePlus signature mechanism requires the requester to perform hash calculation for the request parameters, encrypt them, and send them with the API request to the server. The server uses the same mechanism to perform signature calculation for the received request and compares it with the signature sent by the requester. If the signature does not pass verification, the request will be rejected.

For more information, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
