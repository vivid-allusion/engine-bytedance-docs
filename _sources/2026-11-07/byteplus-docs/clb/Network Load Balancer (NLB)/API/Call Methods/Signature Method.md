---
title: "Signature Method"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Signature-Method"
---

On BytePlus, in order to validate the identity of requesters and prevent API requests from being maliciously tampered with during transmission, a signature mechanism is implemented. It requires the requester to encrypt the request parameters using hashing, and send the hash value with the API request to the server. The server uses the same mechanism to calculate the signature for the received request and then compares it with the one sent by the requester. If the signature verification fails, the request will be rejected.
