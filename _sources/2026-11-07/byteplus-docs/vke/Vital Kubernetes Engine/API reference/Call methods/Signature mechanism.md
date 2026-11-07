---
title: "Signature mechanism"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Signature-method"
---

To ensure the authentication of the identity of the requester and prevent malicious tampering of the request during transmission, the BytePlus signature mechanism requires the requester to perform hashing on the request parameters. After encryption, the hash value is sent to the server together with the API request. The server uses the same mechanism to calculate the signature for the received request and compares it with the signature provided by the requester. If the signature does not pass verification, the request will be rejected. For detailed operations and descriptions, see the BytePlus public documentation [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).
