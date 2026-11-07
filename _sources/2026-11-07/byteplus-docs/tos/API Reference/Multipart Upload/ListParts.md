---
title: "ListParts"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-listparts"
---

<span id="f89653d0"></span>
## **Description**

This API is used to list all uploaded parts associated with an UploadId and returns a maximum of 1,000 parts. 1,000 is the default limit, and you can use the `max-parts` request parameter to further limit the number of returned parts. If your multipart upload involves more than 1,000 parts, the response will contain an `IsTruncated` element with the value `true` and a `NextPartNumberMarker` element. In subsequent `ListParts` requests, you can include a `part-number-marker` query parameter and set its value to the `NextPartNumberMarker` indicated in the previous response.

<span id="caa39863"></span>
## **Request syntax**

```JSON
GET /objectName?uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="aae7171f"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/createmultipartupload).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|uploadId |Query |String |Yes |f93f6fc9da94371f321e1008 |Multipart upload task ID returned in the initialization response, which uniquely identifies the created object. |
|max\-parts |Query |Integer |No |100 |Specifies the maximum number of parts to return. The value can be set to at most 1000, indicating that each response can list up to 1,000 parts. |
|part\-number\-marker |Query |Integer |No |1 |Specifies the part after which listing should begin. Only parts with higher part numbers will be listed. |


<span id="9250e5e3"></span>
## **Request body elements**

No elements are used.

<span id="5b49e4b1"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/createmultipartupload).

<span id="b87af09d"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Bucket |String |Bucket name. |
|Key |String |Object name. |
|UploadId |String |ID of the multipart upload task. |
|MaxParts |Integer |The max\-parts parameter in the request. |
|PartNumberMarker |Integer |The part\-number\-marker parameter in the request. |
|IsTruncated |Bool |Whether the returned list is truncated. Valid values:<br><br><br>* `false`: All results have been returned.<br><br>* `true`: Some results are yet to be returned. |
|NextPartNumberMarker |Integer |Indicates the part\-number\-marker to use in the next request if some results are yet to be returned. |
|StorageClass |String |Storage type of the object created by the multipart upload task. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage. |
|Parts |Array |Root node for part information. |
|PartNumber |Integer |Part number. Parent node: Parts. |
|LastModified |String |Upload time of the part. Parent node: Parts. |
|ETag |String |ETag for the part content. Parent node: Parts. |
|Size |Integer |Part size. Parent node: Parts. |
|Owner |Object |Owner of the multipart upload task. |
|ID |String |Account ID. Parent node: Owner. |
|DisplayName |String |Display name of the account. Parent node: Owner. |


<span id="1b3a2cee"></span>
## **Sample request**

```JSON
GET /objectName?uploadId=UploadId HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 00:15:25 GMT
Authorization: authorization string
```


<span id="66d8fec2"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130c7ea5003e-a444ed0        
x-tos-request-id: 4fac130c7ea5003e-a444ed0            
Date: Fri, 30 Jul 2021 00:15:25 GMT   
server: TosServer
Content-Length: 693

{
    "Bucket": "bucketName",
    "Key": "multiobj1",
    "UploadId": "f93f6fc90d5f371f4f18c0b1",
    "PartNumberMarker": 0,
    "NextPartNumberMarker": 0,
    "MaxParts": 1000,
    "IsTruncated": false,
    "StorageClass": "STANDARD",
    "Owner": {
        "ID": "AccountID"
    },
    "Parts": [
        {
            "PartNumber": 1,
            "LastModified": "2021-08-20T06:43:49Z",
            "ETag": "\"7de47c292287f7965357c1ddd724b2b7\"",
            "Size": 10
        }
    ]
}
```
