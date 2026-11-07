---
title: "Signature mechanism"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Signature_method"
---

To verify the requester identity and prevent malicious tampering during transmission, the BytePlus platform signature mechanism requires the requester to compute a hash of request parameters, encrypt it, and send it with the API request to the server. The server uses the same method to recalculate the signature for the received request and compares it with the requester signature. If the verification fails, the request will be rejected.

For more information, see [Signature request](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
