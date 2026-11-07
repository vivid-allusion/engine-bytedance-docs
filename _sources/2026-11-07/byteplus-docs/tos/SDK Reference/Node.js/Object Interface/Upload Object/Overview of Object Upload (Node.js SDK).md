---
title: "Overview of Object Upload (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-overview-node-js-sdk"
---

The TOS Node.js SDK supports simple upload, shard upload, and other ways to upload files. You can choose the appropriate upload method according to your business needs and the scenarios applicable to different methods.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Upload method description


* [Normal Upload (Node.js SDK)](https://docs.byteplus.com/docs/tos/Normal-upload-node-js-sdk):The maximum file size cannot exceed 5GiB.

* [Append Upload (Node.js SDK)](https://docs.byteplus.com/docs/tos/Append-upload-node-js-sdk):The maximum file size cannot exceed 5GiB.

* [Shard Upload (Node.js SDK)](https://docs.byteplus.com/docs/tos/Shard-upload-node-js-sdk): When the file is large, you can use sharded upload, and the maximum cannot exceed 48.8TiB.

* [Breakpoint Resumption (Node.js SDK)](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-node-js-sdk):Support concurrency, breakpoint continuation, custom sharding size. For large files, it is recommended to use a breakpoint to resume, with a maximum of 48.8TiB.


When uploading objects, the Node.js SDK supports streaming uploads, using the Readable stream as the data source in the upload object interface to upload to the TOS bucket. During the upload process, you can view the upload progress through the progress bar function, and you can use the client side speed limit interface to limit the upload speed.
