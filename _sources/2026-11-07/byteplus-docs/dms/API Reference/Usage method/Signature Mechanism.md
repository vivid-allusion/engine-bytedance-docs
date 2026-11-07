---
title: "Signature Mechanism"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Signature_Mechanism"
---

BytePlus's DMS uses a unified signature mechanism. To ensure the legitimacy of the requester and to prevent malicious tampering during transmission, BytePlus's signature mechanism requires the requester to calculate a hash value for the request parameters, encrypt it, and send it with the API request to the server. The server will use the same mechanism to calculate the signature for the received request and compare it with the signature provided by the requester. If the signature verification fails, the request will be denied. For a detailed description of the signature calculation method, see [Signature Method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).
