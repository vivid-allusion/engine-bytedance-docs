---
title: "Signature method"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Signature-method"
---

BytePlus uses a signature mechanism to verify the identity of requesters and ensure that their requests are not tampered with during transmission. The requesters must calculate the hash value of the request parameter and send the encrypted result along with the API request to the server. The server uses the same mechanism to perform a signature calculation on the received request, and compares the result with the signature passed in by the requester. If the signature fails to pass the verification, the request is declined.

For more information, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request).
