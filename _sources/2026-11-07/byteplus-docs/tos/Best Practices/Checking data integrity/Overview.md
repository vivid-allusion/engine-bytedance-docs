---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview10"
---

During data upload or download using TOS, data inconsistency issues may occur due to network hijacking or data caching outside TOS during public network transmission. TOS offers multiple data consistency features to ensure the consistency of data upload or download. In TOS scenarios, data consistency verification is divided into upload object consistency verification and download object consistency verification. This document introduces the concepts and verification methods for these two scenarios.

<span id=".55u45YWz5qaC5b-1"></span>
## Related concepts

<span id="content-md5"></span>
### Content\-MD5

A standard HTTP request header representing the fingerprint of the request message body data, calculated by applying the MD5 algorithm to the data and then encoding the hash value with Base64 to generate a string.

In TOS scenarios, the PutObject and UploadPart interfaces support carrying this parameter in the request header, while PostObject supports it in the form field. TOS calculates the received data using the same algorithm and compares it with this value. If they do not match, the upload fails, and the object is not generated on the TOS side.

<span id="content-sha256"></span>
### Content\-SHA256

The request header field defined in the TOS scenario is similar to Content\-MD5, also representing the fingerprint of the request message body data. However, it uses a more secure SHA256 algorithm, which calculates the hash value using SHA256 and then encodes it into a string with Hex encoding.

PutObject and UploadPart interfaces support carrying this parameter in the request header field via `x-tos-content-sha256`.

<span id="crc64"></span>
### CRC64

The cyclic redundancy check algorithm is the industry\-standard algorithm commonly used for data verification. For more details, see [Cyclic redundancy check](https://en.wikipedia.org/wiki/Cyclic_redundancy_check).

In the TOS scenario, PutObject, PostObject, UploadPart, GetObject, HeadObject, and CompleteMultipartUpload all return this parameter in the response header field via `x-tos-hash-crc64ecma`, representing the CRC64 checksum of the current read/write data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">CRC64 is a new feature. Objects uploaded before this feature was launched may not have CRC64 included in the response headers of GetObject and HeadObject.</div>


* <div data-tips="true" data-tips-type="warning">When GetObject carries the <code>Range</code> parameter, the returned CRC64 in the response header still represents the CRC64 of the entire object.</div>


* <div data-tips="true" data-tips-type="warning">The object lists retrieved by <a href="https://docs.byteplus.com/docs/tos/reference-listobjects">ListObjects</a> and <a href="https://docs.byteplus.com/docs/tos/reference-listobjectversions">ListObjectVersions</a> also include a new field representing the CRC64 for each object.</div>



<span id=".5qCh6aqM5LiK5Lyg5a-56LGh55qE5LiA6Ie05oCn"></span>
## Verify the consistency of the uploaded object

You can verify the consistency of the uploaded object using Content\-MD5, Content\-SHA256, or CRC64. The comparison of different validation methods is as follows.


|Verification method |Using Content\-MD5 |Using Content\-SHA256 |Using CRC64 |
|---|---|---|---|
|Applicable scenario |* Precompute the MD5 of the data to be uploaded.<br><br>* For relatively small data uploads, such as data sizes within 10 MB, otherwise precomputation costs are high.<br><br>* Data verification fails; scenarios where you do not want TOS to create an object. |* Knowing the SHA256 of the data to be uploaded in advance.<br><br>* The data to be uploaded is relatively small, such as within 10 MB, otherwise the pre\-calculation cost is high.<br><br>* When data validation fails and you do not want TOS to generate the object.<br><br>* When you want to use a more secure hashing algorithm for data validation. |* CRC64 can be calculated simultaneously during data upload without additional calculation overhead.<br><br>* For multipart uploads, comparing the CRC64 of the merged final object provides more reliable verification. |
|drawbacks |* Calculating the MD5 of the data to be uploaded in advance incurs some cost.<br><br>* The security of the MD5 algorithm is lower than that of the SHA256 algorithm. |* SHA256 of the data to be uploaded must be calculated in advance, which incurs some cost.<br><br>* The efficiency of the SHA256 algorithm is lower than that of the MD5 algorithm. |The verification process is completed on the client side. By then, TOS has already created the actual uploaded object, requiring additional cleanup such as overwriting or deleting. |
|Supported APIs |* PutObject<br><br>* PostObject<br><br>* UploadPart |* PutObject<br><br>* UploadPart |* PutObject<br><br>* PostObject<br><br>* UploadPart<br><br>* CompleteMultipartUpload |
|Reference |[using Content-MD5](https://docs.byteplus.com/en/docs/tos/Verify-consistency-of-the-uploaded-object#.6YCa6L-HY29udGVudC1tZDU=) |[using Content-SHA256](https://docs.byteplus.com/en/docs/tos/Verify-consistency-of-the-uploaded-object#.6YCa6L-HY29udGVudC1zaGEyNTY=) |[Using CRC64](https://docs.byteplus.com/en/docs/tos/Verify-consistency-of-the-uploaded-object#.6YCa6L-HY3JjNjQ=) |
|Recommendations |* If you want to avoid additional computational overhead, prioritize using the CRC64 validation method.<br><br>* If you want no object generated on the TOS side when data is inconsistent and prefer a more secure hashing algorithm, use the Content\-SHA256 validation method; otherwise, use the Content\-MD5 validation method. |||


<span id=".5qCh6aqM5LiL6L295a-56LGh55qE5LiA6Ie05oCn"></span>
## Validate the consistency of the downloaded object

You can use CRC64 to verify the consistency of the downloaded object. For detailed information, see [Validate the consistency of the downloaded object](https://docs.byteplus.com/en/docs/tos/Verify-the-consistency-of-the-downloaded-object).
