---
title: "Overview of Object Uploading (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-overview-java-sdk"
---

The Java SDK supports multiple methods for uploading data. The following section provides a brief overview of the parameter constraints for each upload method.

<span id=".5LiK5Lyg6K-05piO"></span>
## Upload Instructions


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-java-sdk): The size of an individual upload object must not exceed 5GiB.

* [Append Upload](https://docs.byteplus.com/docs/tos/Append-upload-java-sdk): Each append must be at least 128 KiB in size, and the total size of a single object after appending must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-java-sdk): When the file size is large, it is recommended to use multipart upload. The size of all fragments except the final one must be greater than or equal to 5 MiB. The numbering of uploaded fragments is also subject to a range constraint, specifically [1,10000].

* [Resumable Upload](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-java-sdk): For large local files, it is recommended to use the resumable upload method, which supports concurrent uploads, progress bars, resumable upload capability, and allows configuration of concurrency and chunk size.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For all the upload methods described above, the TOS Java SDK consistently uses the InputStream class as the data stream parameter for uploading. You may use different types of data streams according to business requirements, such as ByteArrayInputStream, FileInputStream, etc. Subsequent chapters will provide usage instructions and sample code for uploading different data streams for your reference.</div>


* <div data-tips="true" data-tips-type="tip">During data upload, the SDK emits progress events, which you may monitor according to your business requirements. Subsequent chapters will provide explanations and sample code for monitoring upload progress events for your reference.</div>


* <div data-tips="true" data-tips-type="tip">During data upload, the SDK restricts the available upload bandwidth. You may configure this setting according to your business requirements. Subsequent chapters will provide usage instructions and sample code for upload client rate limiting for your reference.</div>
