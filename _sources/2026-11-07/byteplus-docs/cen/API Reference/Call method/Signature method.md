---
title: "Signature method"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Signature-method"
---

To ensure the authenticity of the requester's identity and prevent malicious tampering during transmission, the platform's signature mechanism requires the requester to calculate a hash value of the request parameters. This hash is encrypted and sent to the server along with the API request. The server then performs the same signature calculation on the received request and compares it with the signature provided by the requester. If the signature fails verification, the request will be rejected.

For details, see [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).
