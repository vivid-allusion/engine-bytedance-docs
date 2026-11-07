---
title: "Bucket type"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-type"
---

TOS has two types of buckets: FNS and HNS. This topic explains the differences and things to consider.

<span id="6f9e4bfa"></span>
## FNS

A flat namespace (FNS) bucket is a storage space provided by TOS for storing large amounts of data. It supports features such as lifecycle management and back\-to\-origin.

<span id="e5d34025"></span>
## HNS

A hierarchical namespace (HNS) bucket is a new type of bucket introduced by TOS. It uses a hierarchical structure to organize metadata. Besides its hierarchical namespace features, an HNS bucket can scale as much as an FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

HNS buckets can do everything FNS buckets can do, plus more. They support directory\-level mv and rename operations. They also improve common read operations, like List and Head for directories, to make data processing more efficient and faster. This makes them well\-suited for use cases in big data, data lakes, and AI.

Learn more in [What is hierarchical namespace](https://docs.byteplus.com/docs/tos/What-is-hierarchical-namespace).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For supported regions for HNS buckets, see<a href="https://docs.byteplus.com/en/docs/tos/What-is-hierarchical-namespace#a9f27159"> Supported regions</a>.</div>
