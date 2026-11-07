---
title: "Overview of Downloading Objects (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object-overview4"
---

The TOS Node.js SDK supports downloading objects through direct download or range download, etc. You can choose the appropriate download method according to your business needs and the scenarios applicable to different methods.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Download method description


* [Normal Download (Node.js SDK)](https://docs.byteplus.com/docs/tos/Normal-download-node-js-sdk): Downloads the entire object directly from the specified bucket.

* [Limited Download (Node.js SDK)](https://docs.byteplus.com/docs/tos/Limited-download-node-js-sdk): If the qualification is met, it will be downloaded. If it is not met, an exception will be thrown and the download behavior will not be triggered.

* [Scope Download (Node.js SDK)](https://docs.byteplus.com/docs/tos/Scope-download-node-js-sdk):You don't need to download the entire object, but only some of the information in the object. You can use range download to download data within a specified range.

* [Breakpoint Resume Download (Node.js SDK)](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-node-js-sdk):When downloading an object, the download fails due to network abnormalities or program crashes. You can use the breakpoint to resume the download and continue to download unsuccessful files.


When downloading objects, the Node.js SDK supports streaming downloads, and returns a Readable stream as a data source on the download object interface for reading. During the download process, you can view the download progress through the progress bar function, and you can use the client side speed limit interface to limit the download speed.
