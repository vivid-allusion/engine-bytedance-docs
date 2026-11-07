---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-overview"
---

Torch Object Storage (TOS) is a highly reliable and available object storage system, featuring low latency, cost effectiveness, and massive data capacity, thereby enabling flexible data management. This topic describes TOS APIs and their request parameters with use examples. You can create and delete buckets, upload, download, and delete objects, and perform many more operations using these APIs.

<span id="8c541cf9"></span>
## **Instructions**

For all operations supported by TOS, see [API Overview](https://docs.byteplus.com/en/tos/reference/api-overview).

The topic focuses on request syntax, meaning of parameters, and sample requests and responses.

<span id="f410dc90"></span>
## **TOS terms**


|**Term** |**Description** |
|---|---|
|Bucket |A globally unique namespace in TOS that acts as a container for storing object data. You must create a bucket before uploading objects to TOS. |
|Object |A fundamental unit that uniquely identifies a piece of data in a bucket, comprising metadata, data, and a name. |
|Region |The physical location of a TOS data center. |
|User |A service consumer created by an account, possessing identity credentials (passwords and access keys). |
|Endpoint |An endpoint for TOS to provide external services. |
|Access Key ID (AK) |The ID of an access key. A unique identifier paired with the SK to obtain an encrypted signature for a request. |
|Secret Access Key (SK) |A private access key paired with the AK to obtain an encrypted signature for a request, thus identifying the sender and ensuring request integrity. |
