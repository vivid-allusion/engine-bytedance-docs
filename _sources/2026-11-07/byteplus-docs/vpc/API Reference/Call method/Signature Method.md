---
title: "Signature Method"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Signature-method"
---

On BytePlus, in order to validate the identity of requesters and prevent API requests from being maliciously tampered with during transmission, a signature mechanism is implemented. It requires the requester to encrypt the request parameters using hashing, and send the hash value with the API request to the server. The server uses the same mechanism to calculate the signature for the received request and then compares it with the one sent by the requester. If the signature verification fails, the request will be rejected.

For more information, refer to [Signing method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
