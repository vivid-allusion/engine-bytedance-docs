---
title: "Signature method"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Signature-method"
---

All requests to the PrivateLink API must be signed to authenticate the sender and ensure request integrity. The API uses an HMAC signature scheme where request parameters are hashed using a secret key. The hashed signature is included in the request header or parameter. Upon receipt, the server recalculates the signature using the same key and parameters and compares it with the sent signature. Requests with an invalid or mismatching signature will be rejected.

For more information, refer to [Signature method ](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
