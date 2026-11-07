---
title: "Overview of Object Download (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object-overview-go-sdk"
---

The TOS Go SDK supports downloading objects through methods such as direct download and range download. You can select the appropriate download method according to your business requirements and the scenarios where each method is applicable.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Instructions for Download Methods


* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-go-sdk): Directly download the entire object from the specified bucket.

* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-go-sdk): The download will proceed only if the specified conditions are met; otherwise, an exception will be thrown and the download will not be triggered.

* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-go-sdk): You do not need to download the entire object. If you only need part of the information in the object, you can use range download to download data within the specified range.

* [Resumable Download](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-go-sdk): When downloading an object, if the download fails due to network interruptions or program crashes, you can use the resumable download feature to continue downloading files that were not successfully downloaded.


When downloading objects, the Go SDK supports streaming downloads by returning io.Reader from the download object interface as the data source for reading. During the download process, users can monitor the progress via the progress bar feature. The client\-side throttling interface can be used to restrict the download speed.
