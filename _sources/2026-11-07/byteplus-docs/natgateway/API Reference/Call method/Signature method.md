---
title: "Signature method"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Signature-method"
---

To ensure requesters have valid identities and their requests are not maliciously tampered with during transmission, the signature mechanism of BytePlus requires a requester to calculate the hash value of the request parameter and send the encrypted result together with the API request to the server. The server uses the same mechanism to perform a signature calculation on the received request, and compares the result with the signature passed in by the requester. If the signature fails to pass the verification, the request is declined.

For more information, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
