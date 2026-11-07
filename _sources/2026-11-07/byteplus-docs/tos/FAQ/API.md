---
title: "API"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/API"
---

This article introduces common issues encountered when using the TOS API.

<span id=".5aaC5L2V5Yik5pat5a-56LGh5piv5ZCm5Li655uu5b2V77yf"></span>
### How to determine if an object is a directory?

The TOS service itself does not have the concept of directories; all objects are stored flat under the bucket. To simulate directories within a TOS bucket, it is generally agreed that objects with names ending with`/`a slash (/) (regardless of the object size) represent a directory.

<span id=".5aaC5L2V5L2_55SoLWFwaS3liJfkuL7nm67lvZXvvJ8="></span>
### How to list directories using the API?

The TOS service itself does not have the concept of directories; it is generally agreed that objects with names ending with`/`a slash (/) (regardless of the object size) represent a directory. When using the TOS API to list objects, you can pass the delimiter (`delimiter`) parameter to simulate directory\-style listing.

After setting this delimiter, the response body of the list objects interface will include the following information


* `CommonPrefixes` array: represents and returns a collection of subdirectories.

* `Contents` array: represents the collection of objects contained in the current directory.


You can use the subdirectory contained in CommonPrefixes as the prefix (`prefix`) parameter to sequentially list the subdirectory’s collections of subdirectories and objects. For more information about the list objects interface, see [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).

<span id=".bGlzdG9iamVjdHMt5o6l5Y-j5pSv5oyB5YCS5bqP5p-l6K-i5ZCX77yf"></span>
### Does the ListObjects interface support reverse order queries?

It does not support this; it only provides forward lexicographical queries by object name, based on prefix and delimiter (usually`/`)

<span id=".5aaC5L2V6I635Y-W5qG25YaF55uu5b2V5aSn5bCP5ZKM5paH5Lu25Liq5pWw77yf"></span>
### How to get the directory size and file count inside a bucket?

The TOS service itself does not have the concept of directories and therefore does not provide an interface to get the directory size and file count inside a bucket. If you need to obtain the size and number of files in a bucket directory, you can use the ListObjects API to sequentially calculate the directory size and file count in the bucket. For more information, see [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).

<span id=".5piv5ZCm5o-Q5L6b5LiK5Lyg44CB5LiL6L295Y-K5Yig6Zmk55uu5b2VLWFwae-8nw=="></span>
### Are APIs provided for uploading, downloading, and deleting directories?

The TOS service itself does not have the concept of directories, so it does not provide APIs for uploading, downloading, or deleting directories. If you need to upload, download, or delete directories, you can achieve this through the following APIs:


* Upload directory: use [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects) and [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).

* Download directory: use [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects) and [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).

* Delete directory: use [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects) and [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).


<span id=".5aaC5L2V6YCa6L-HLWFwaS3lrp7njrDlr7nosaHph43lkb3lkI3vvIhyZW5hbWXvvInvvJ8="></span>
### How to rename objects through the API?

The TOS service currently does not provide an API for renaming objects. To achieve this, you can call CopyObject and DeleteObject sequentially. In addition, for large objects exceeding 5 GB, directly calling CopyObject will fail; you need to use UploadPartCopy for segmented copying.

<span id=".Y29weW9iamVjdC3mjqXlj6PmmK_lkKbkvJrljaDnlKjluKblrr3phY3pop3vvJ_mmK_lkKbmlK_mjIHluYLnrYnvvJ8="></span>
### Does the CopyObject interface consume bandwidth quota? Does it support idempotency?

The CopyObject interface uses isolated internal bandwidth and does not consume your read/write bandwidth quota. It is idempotent, so client retransmissions due to timeout will not cause data corruption.

<span id=".Z2V0b2JqZWN0LeaOpeWPo-aYr-WQpuaUr-aMgemAmui_hy1vZmZzZXQtbGVuZ3RoLeeahOaWueW8j-iOt-WPluWvueixoeWGheWuueeahOafkOS4gOauteaVsOaNru-8nw=="></span>
### Does the GetObject interface support retrieving a specific segment of the object content using offset+length?

The GetObject interface implements the standard HTTP Range Get protocol. You can include `Range: bytes=x-y` in the request header to fetch part of the object content. For more details, see the [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).

<span id=".5aaC5L2V6YCa6L-HLWFwaS3liKTmlq3lr7nosaHmmK_lkKblj5HnlJ_lj5jljJbvvJ8="></span>
### How to determine if an object has changed via API?

The TOS service provides the HeadObject interface to query object metadata. When the object exists, the response header returns `ETag` and `Last-Modified`, representing the object's data hash and last upload time.

When using GetObject or CopyObject interfaces, you can use the HTTP header syntax If\-Match or If\-Unmodified\-Since to ensure operations execute only if the object has not changed.

<span id=".5aaC5L2V6YCa6L-HLWFwaS3lsIblr7nosaHku47kuIDkuKrmobYt6LSm5Y-36L2s5a2Y5Yiw5Y-m5LiA5Liq5qG2Lei0puWPt--8nw=="></span>
### How to transfer an object from one bucket/account to another via API?


* same region: it is recommended to use the CopyObject or UploadPartCopy API to copy objects directly. the differences are as follows:

   * CopyObject supports only objects smaller than 5 GiB.

   * UploadPartCopy supports objects larger than 5 GiB through multipart copying.

* cross\-region: copying requires combining GetObject and PutObject/UploadPart to read and write simultaneously.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">when transferring within the same region or across regions, ensure you have read permission for the source bucket and write permission for the target bucket.</div>


<span id=".5aaC5L2V6YCa6L-HLWFwaS3kv67mlLnlr7nosaHlrZjlgqjnsbvlnovvvJ8="></span>
###  How to change the storage class of an object via API?


* for objects smaller than 5 GiB: use CopyObject.

* for objects larger than 5 GiB: use CreateMultipartUpload, UploadPartCopy, and CompleteMultipartUpload.


<span id=".5L2_55So6aKE562-5ZCNLXVybC3or7fmsYItdG9zLWFwaS3miqXplJktNDAzLeaYr-S4uuS7gOS5iO-8nw=="></span>
### why does requesting the TOS API with a pre\-signed URL return error 403?

403 errors usually occur because the key fields involved in the signature do not match the fields actually sent in the HTTP request, such as the method name (GET/HEAD/PUT/POST/DELETE), request query parameters, request headers, etc. For more information, see [URL with signature](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).

<span id=".6aKE562-5ZCNLXVybC3nmoTmnInmlYjmnJ_mmK_lpJrkuYXvvJ8="></span>
### What is the validity period of a pre\-signed URL?

The TOS server supports pre\-signed URLs with a maximum validity of 7 days. For methods to generate pre\-signed URLs, see [URL with signature](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url). It is recommended to use the PreSignedURL function of the [TOS SDK](https://docs.byteplus.com/docs/tos/SDK-overview) to generate pre\-signed URLs.
