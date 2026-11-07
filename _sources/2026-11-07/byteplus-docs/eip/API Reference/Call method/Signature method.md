---
title: "Signature method"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Signature-method"
---

To verify the requester's identity and prevent malicious tampering during transmission, BytePlus signature mechanism requires the requester to compute a hash of request parameters, encrypt it, and send it with the API request to the server. The server uses the same method to recalculate the signature for the received request and compares it with the requester's signature. If the verification fails, the request will be rejected.

For more information, refer to [Signing method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
