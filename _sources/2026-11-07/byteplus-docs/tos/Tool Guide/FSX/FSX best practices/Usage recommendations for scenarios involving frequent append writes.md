---
title: "Usage recommendations for scenarios involving frequent append writes"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Usage-recommendations-for-scenarios-involving-frequent-append-writes"
---

In scenarios such as log file recording, data archiving, and backup, it is often necessary to frequently perform append writes to files to facilitate subsequent analysis and processing. This article explains the working principles of append writing and provides recommendations for scenarios involving frequent append operations, helping you write data efficiently and reliably.

<span id="4470d3c0"></span>
### Working Principle

The FSX tool employs different underlying implementation principles for append write operations depending on the type of storage bucket. The specific details are as follows:


* When appending data to objects in an FNS bucket, historical data stored in the cloud is copied from TOS using the UploadPartCopy interface, while newly appended data is uploaded using either the UploadPart or PutObject interface. In this scenario, only one flush operation is supported per open operation.

* When appending data to objects in an HNS bucket, TOS uses the AppendObject interface to perform the append operation. In this scenario, multiple flush operations can be performed on objects written in append mode.


<span id="ec1500b9"></span>
## Usage Recommendations

When performing append writes to FNS bucket objects, each append write operation requires first executing an open operation, followed by a flush operation, and each open operation allows only one flush operation. When appending to HNS bucket objects, it is not necessary to re\-open after each flush operation; after a single open operation, multiple flush operations can be performed.

Since HNS supports an append write mechanism with multiple flush operations, to avoid request amplification and performance degradation caused by frequent open and flush calls, it is recommended to prioritize the use of HNS buckets in scenarios involving frequent append writes. For a detailed introduction to HNS buckets, please refer to [What Is Hierarchical Namespace](https://docs.byteplus.com/docs/tos/What-is-hierarchical-namespace).
