---
title: "Overview of Downloadable Objects (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object-overview-java-sdk"
---

The TOS Java SDK supports multiple methods for downloading objects, including standard download and range download. You may select the most suitable download method according to your business requirements and the applicable scenarios for each approach.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Download Method Instructions


* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-java-sdk): generally used for downloading small objects.

* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-java-sdk): When you only need to download a portion of an object's data, you can use range download.

* [Resumable Download](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-java-sdk): When downloading large files, you can use resumable download.

* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-java-sdk): The download will proceed only if the specified conditions are met; if not, an exception will be thrown and the download action will not be triggered.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For all of the above download methods, the TOS Java SDK consistently uses InputStream as the return type. You may utilize it according to your business requirements, such as downloading it to a local file, reading it directly in memory, etc. Subsequent chapters will provide instructions for using the data stream returned by downloads, along with sample code for your reference.</div>


* <div data-tips="true" data-tips-type="tip">During the data download process, the SDK will emit progress events, which you can listen to according to your business requirements. Subsequent chapters will provide explanations and sample code on download progress event listening for your reference.</div>


* <div data-tips="true" data-tips-type="tip">During data download, the SDK restricts the download bandwidth. You can configure the bandwidth limit according to your business requirements. Subsequent chapters will provide usage instructions and sample code for download client speed limiting, for your reference.</div>
