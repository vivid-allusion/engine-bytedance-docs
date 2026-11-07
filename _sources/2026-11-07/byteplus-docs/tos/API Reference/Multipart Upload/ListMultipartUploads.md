---
title: "ListMultipartUploads"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-listmultipartuploads"
---

<span id="fcb4c8c9"></span>
## **Description**

This API is used to list in\-progress multipart upload tasks, which are tasks that have been initialized using [CreateMultiPartUpload](https://docs.byteplus.com/en/tos/reference/createmultipartupload) but have not been merged or completed.

This action returns at most 1,000 multipart uploads in the response. 1,000 is the maximum and default number of uploads a response can include. You can further limit this number in a response by specifying the `max-uploads` parameter in the request. If some multipart uploads are yet to be listed, the response will contain an `IsTruncated` element with the value `true`. To list these multipart uploads, use the key\-marker and `upload-id-marker` request parameters.

<span id="c0ec8112"></span>
## **Request syntax**

```JSON
GET /?uploads HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="7eab7f64"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|uploads |Query |String |Yes | |Identifies a ListMultipartUploads request. |
|delimiter |Query |String |No |/ |Specifies the character used to group the object keys,which is usually a forward slash ( / ). |
|encoding\-type |Query |String |No |url |Specifies the encoding of the returned content. Valid value:<br><br><br>* `url`: Use URL encoding. |
|max\-uploads |Query |Integer |No |100 |Specifies the maximum number of multipart upload tasks to return. The value can be set to at most 1000, indicating that each response can list up to 1,000 tasks. |
|prefix |Query |String |No |aaa |Specifies to list in\-progress uploads only for those keys that begin with the specified prefix. You can use prefixes to group objects in the bucket (similar to using a folder). |
|key\-marker |Query |String |No |test.txt |Used with upload\-id\-marker. If upload\-id\-marker is not specified, TOS returns multipart uploads with a key lexicographically greater than the specified key\-marker. If upload\-id\-marker is specified, any multipart uploads for a key equal to the key\-marker might also be included, provided they have an upload ID lexicographically greater than the specified upload\-id\-marker. |
|upload\-id\-marker |Query |String |No |f93f6fc9da94371f321e1008 |Used with key\-marker. If key\-marker is not specified, this parameter is ignored. Otherwise, any multipart uploads for a key equal to the key\-marker might also be included in the list, provided they have an upload ID lexicographically greater than the specified upload\-id\-marker. |


<span id="604b2dab"></span>
## **Request body elements**

No elements are used.

<span id="05a9d15a"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="0d1d2381"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Bucket |String |Bucket name. |
|KeyMarker |String |The key\-marker parameter in the request. |
|UploadIdMarker |String |The upload\-id\-marker parameter in the request. |
|MaxUploads |Integer |The max\-uploads parameter in the request. |
|Prefix |String |The prefix parameter in the request. |
|Delimiter |String |The delimiter parameter in the request. |
|EncodingType |String |The encoding\-type parameter in the request. |
|IsTruncated |Bool |Whether the returned list is truncated. Valid values:<br><br><br>* `false`: All results have been returned.<br><br>* `true`: Some results are yet to be returned. |
|NextKeyMarker |String |Indicates the key\-marker value to use in the next request if some results are yet to be returned. |
|NextUploadIdMarker |String |Indicates the upload\-id\-marker value to use in the next request if some results are yet to be returned. |
|CommonPrefixes |Array |If the request specifies a delimiter, the response will contain the CommonPrefixes element,which summarizes object keys that have the same substring between the prefix and the next occurrence of the delimiter into respective groups. |
|Uploads |Array |Root node for multipart upload tasks. |
|Key |String |Object name. Parent node: Uploads. |
|UploadId |String |ID of the multipart upload task. Parent node: Uploads. |
|StorageClass |String |Storage type of the object created by the multipart upload task. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br><br>Parent node: Uploads. |
|Initiated |String |Initialization time of the multipart upload task. Parent node: Uploads. |
|Owner |Object |Owner of the multipart upload task. Parent node: Uploads. |
|ID |String |Account ID. Parent node: Owner. |
|DisplayName |String |Display name of the account. Parent node: Owner. |


<span id="24c30ecd"></span>
## **Sample request**

```JSON
GET /?uploads HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 00:13:04 GMT
Authorization: authorization string
```


<span id="41a0eba2"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 582a920a02840016-a444ed0
x-tos-request-id: 582a920a02840016-a444ed0
Date: Fri, 30 Jul 2021 00:13:04 GMT
server: TosServer
Content-Length: 636

{
    "Bucket": "bucketName",
    "KeyMarker": "",
    "UploadIdMarker": "",
    "NextKeyMarker": "",
    "NextUploadIdMarker": "",
    "Delimiter": "",
    "Prefix": "",
    "MaxUploads": 1000,
    "IsTruncated": false,
    "Uploads": [
        {
            "Key": "multiobj1",
            "UploadId": "f93f6fc90d5f371f4f18c0b1",
            "Owner": {
                "ID": "AccountID",
                "DisplayName": "DisplayName"
            },
            "StorageClass": "Standard",
            "Initiated": "2021-08-20T06:43:36.000Z"
        }
    ],
    "CommonPrefixes": null
}
```
