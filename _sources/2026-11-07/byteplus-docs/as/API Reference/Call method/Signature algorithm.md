---
title: "Signature algorithm"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Signature-method"
---

To verify the requester identity and prevent malicious tampering during transmission, BytePlus signature mechanism requires the requester to compute a hash of request parameters, encrypt it, and send it with the API request to the server. The server uses the same method to recalculate the signature for the received request and compares it with the requester signature. If the verification fails, the request will be rejected.

For details, see [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) documentation.
