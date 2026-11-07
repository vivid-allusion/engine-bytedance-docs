---
title: "Signature Method"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Signature_Method"
---

To ensure the legitimacy of the requester's identity and to prevent malicious tampering of the request during transmission, the signature mechanism of BytePlus requires the requester to calculate the hash value of the request parameters. After encryption, the request parameters are sent to the server together with the OpenAPI request. The server will calculate the signature of the received request based on the same mechanism and compare it with the signature offered by the requester. If the signature fails to pass the verification, it will be rejected. Please refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) Documentation.
