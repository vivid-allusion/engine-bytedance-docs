---
title: "Presigned Overview (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Presignature-overview-go-sdk"
---

You can add signature information to the query parameters of the URL. This URL contains information such as AK, validity period, resource, operation, and signature. Anyone who uses this URL within the validity period can perform the operation associated with the URL. This method is called pre\-signature.


* [Standard Pre-signed Link](https://docs.byteplus.com/docs/tos/Normal-pre-signature-go-sdk): You can access the TOS service by generating a pre\-signed link using the Go SDK.

* [Post Form Pre-Signature](https://docs.byteplus.com/docs/tos/Post-form-pre-signature-go-sdk): TOS supports browser\-based POST object upload requests, enabling you to upload content directly to TOS. You can use the Go SDK to generate Post form pre\-signature parameters.
