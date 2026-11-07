---
title: "Common Concepts"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-common-concepts"
---

<span id="0ed5aa50"></span>
## **Bucket**


* A bucket is a container for storing objects. All objects must belong to a bucket. A bucket has various configuration attributes, including region and access permission. You can create different types of buckets to store different data as needed.

   * Bucket names are globally unique. After you create a bucket, other users cannot create a bucket with the same name as the bucket you create.

   * The storage capacity of each bucket is not limited.

* A bucket name should conform to the following conventions:

   * It can contain lowercase letters, digits, and hyphens ( \- ) only.

   * It can start and end with digits or lowercase letters only.

   * It must contain 3–63 characters.


<span id="fa263681"></span>
## **Object**


* An object (or a file) is a basic storage unit in TOS. It consists of a key, data, and metadata.

* An object key is the full name of an object uploaded to a bucket, that is, a full path containing the directory and suffix, such as `abc/xyz/test123.txt`.

* An object name should conform to the following conventions:

   * It must be UTF\-8 encoded.

   * It must contain 1–1,024 bytes.

   * It cannot start with backslashes ( \ ).

   * It cannot contain `\a`, `\b`, `\t`, `\n`, `\v`, `\f`, or `\r`.


<span id="18f8c2ba"></span>
## **Region**

A region is the physical location of a TOS data center. For more information on the list of available regions for TOS, see [Region and Endpoint](https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0).

<span id="97dc55da"></span>
## **Access key**

An access key (AK) consists of an access key ID and secret. It is your credential to access TOS.

<span id="6c5eccec"></span>
## Strong Consistency

TOS has strong consistency, which means that read and write operations on the same object can always present a consistent state at any given time. After successfully writing an object to TOS, any subsequent read operation can immediately access the latest written data. Even if there are multiple copies or distributed storage nodes, the system ensures that data is synchronized and immediately accessible in all copies.
