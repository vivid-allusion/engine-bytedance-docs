---
title: "About the request signature"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-signature"
---

To ensure the validity of API requests and to protect the API requests from being maliciously tampered during transmission, BytePlus signature mechanism requires clients to calculate a signature for the request parameters, then transmit the signature to the API server together with the API request for verification. If the signature verification fails, the request will be rejected by the server.
