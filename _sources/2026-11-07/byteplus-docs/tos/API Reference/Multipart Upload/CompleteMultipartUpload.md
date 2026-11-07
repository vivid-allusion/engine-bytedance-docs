---
title: "CompleteMultipartUpload"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-completemultipartupload"
---

<span id="ad284eed"></span>
## **Description**

This API is used to merge uploaded parts. To call this API, you must provide a valid part list (including `PartNumber` and `ETag`). Upon receiving your request, TOS merges the parts specified in the part list into an object.

<span id="d967a718"></span>
## **Instructions**


* Initialization can be performed multiple times for the same object, generating different `UploadIds`. An `UploadId` will be deleted after the associated parts have been successfully merged, and other `UploadIds` are not affected.

* `PartNumber` can be any number from 1 to 10,000, inclusive. PartNumbers will be verified before the merge, which must involve each uploaded part.

* The merged parts are combined into a new object, which, like an ordinary object, can be deleted using an object deletion API and becomes unrecoverable thereafter.


<span id="4d0529a3"></span>
## **Request syntax**

```JSON
POST /objectName?uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: length

{
    "Parts":[{
        "PartNumber":partNumber, 
        "ETag":etag
    }]
}
```


<span id="be90aaf6"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|uploadId |Query |String |Yes |f93f6fc9da94371f321e\*\*\*\* |Identifies a multipart upload task. |
|x\-tos\-forbid\-overwrite |Header |String |No |false |Indicates whether overwriting an object with the same name is allowed, with the following values explained:<br><br><br>* Not specifying or specifying as `false`: allows overwriting Objects with the same name.<br><br>* Specifying as `true`: prohibits overwriting Objects with the same name.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the destination Bucket has versioning enabled or suspended, the <code>x-tos-forbid-overwrite</code> parameter is ignored, allowing overwriting Objects with the same name.</div><br> |
|if\-match |Header |String |No |d41d8cd98f00b204e9800998ecf8427e |ETag condition controlling upload behavior: the object only uploads if the specified ETag matches the existing object's ETag in the bucket. If the specified ETag does not exist or does not match, the upload fails and returns a 412 status code. |
|if\-none\-match |Header |String |No |d41d8cd98f00b204e9800998ecf8427e |ETag condition controlling upload behavior: the object uploads only if the specified ETag does not match the ETag of the existing object in the bucket. If the ETag of the existing object in the bucket matches the specified ETag, the upload fails and returns status code 412.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>if-none-match</code> supports setting to<code>*</code>, which means the upload fails and returns status code 412 if an object with the same name exists in the target bucket, regardless of its ETag.</div><br> |


<span id="97672bb2"></span>
## **Request body elements**

The request body specifies a list of parts to merge.


|**Name** |**Description** |
|---|---|
|Parts |Uploaded parts. |
|PartNumber |Number of an uploaded part. Parent node: Parts. |
|ETag |ETag of the part returned upon successful upload. Parent node: Parts. |


<span id="882a634b"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-server\-side\-encryption |String |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |When SSE\-KMS encryption is used for the object, this header is returned, indicating the KMS master key ID used for SSE\-KMS encryption. |
|x\-tos\-version\-id |String |Version ID of the created object. This header will not appear in the response if the object has no version ID. |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This is the CRC\-64 value of the unencrypted object content when server\-side encryption is enabled for object upload.</div><br> |


<span id="bc676150"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Location |String |URL for the newly created object, including a domain name. |
|Bucket |String |Bucket name. |
|Key |String |Name of the resulting object. |
|ETag |String |ETag generated at object creation that uniquely identifies the object content. |


<span id="f1631a6c"></span>
## **Sample request**

```JSON
POST /objectName?uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:38 GMT
Authorization: authorization string
Content-Length: 100

{
    "Parts":[{
        "PartNumber":1, 
        "ETag":"7de47c292287f7965357c1ddd724b2b7"
    }]
}
```


<span id="3ed4754a"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 9b84750a5bbc0029-a444ed0
x-tos-request-id: 9b84750a5bbc0029-a444ed0
Date: Fri, 30 Jul 2021 13:59:38 GMT
server: TosServer
Content-Length: 235

{
    "Location": "http://bucketName.tos-ap-southeast-1.bytepluses.com/objectName",
    "Bucket": "bucketName",
    "Key": "objectName",
    "ETag": "\"00b8d61d63ca2bbc2b535917e40ef478-1\""
}
```
