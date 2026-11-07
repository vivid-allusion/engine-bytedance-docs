---
title: "Signature method"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Signature-method"
---

To ensure the legitimacy of the requester's identity and protect the request from being maliciously tampered with during transmission, the BytePlus signature mechanism requires the requester to compute a hash value of the request parameters, encrypt it, and send it together with the API request to the server. The server will perform the same signature calculation on the received request and compare it with the signature provided by the requester. If the signature fails verification, the request will be rejected.

See [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).
