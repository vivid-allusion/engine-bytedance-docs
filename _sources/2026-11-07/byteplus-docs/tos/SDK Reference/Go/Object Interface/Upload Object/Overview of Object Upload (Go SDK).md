---
title: "Overview of Object Upload (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-overview-go-sdk"
---

The TOS Go SDK supports multiple file upload methods, including simple upload and multipart upload. You may select the most suitable upload method according to your business requirements and the scenarios in which each method is applicable.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Description of Upload Methods


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-go-sdk): The maximum file size must not exceed 5GiB.

* [Additional Upload](https://docs.byteplus.com/docs/tos/Append-upload-go-sdk): The maximum file size must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-go-sdk): When handling large files, multipart upload can be used, with a maximum file size that cannot exceed 48.8 TiB.

* [Resumable Upload](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-go-sdk): Supports concurrent operations, resumable upload, and customizable chunk size. For large files, it is recommended to use resumable transfer. The maximum file size must not exceed 48.8 TiB.


When uploading objects, the Go SDK supports streaming uploads, allowing data to be uploaded to a TOS bucket via the upload object interface using io.Reader as the data source. During the upload process, users can monitor the progress via the progress bar feature. The client\-side throttling interface may be used to restrict the upload speed.
