---
title: "Signature Method"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Signature-method"
---

In order to validate the identity of requesters and prevent API requests from being maliciously tampered with during transmission, a signature mechanism is implemented. It requires the requester to encrypt the request parameters using hashing, and send the hash value with the API request to the server. The server uses the same mechanism to calculate the signature for the received request and then compares it with the one sent by the requester. If the signature verification fails, the request will be rejected.

For more information, refer to [Signature method](https://docs.byteplus.com/en/docs/6369/67269).
