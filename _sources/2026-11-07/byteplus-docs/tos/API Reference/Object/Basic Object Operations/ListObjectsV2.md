---
title: "ListObjectsV2"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-listobjectsv2"
---

<span id="19cc1b6f"></span>
## **Description**

This API is used to list objects in a bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ListObjectsV2 is an upgraded version of ListObjects, offering more parameters and addressing the timeout issue of the latter.</div>


<span id="97362c43"></span>
## **Restrictions**


* To use it, you must have read access to the bucket.

* A single request to the bucket returns up to 1,000 objects. You can use the `max-keys` parameter to adjust the number of objects returned.


<span id="d2e6ba17"></span>
## **Request syntax**

```JSON
GET /?list-type=2 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="395b27de"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|list\-type |Query |Integer |Yes |2 |The value `2` instructs to use the ListObjectsV2 API to list the bucket objects. |
|delimiter |Query |String |No |/ |Specifies the character used to group the object keys,which is usually a forward slash ( / ). |
|encoding\-type |Query |String |No |url |Specifies the encoding of the returned content. The value `url` indicates URL encoding. |
|max\-keys |Query |Integer |No |100 |Specifies the maximum number of objects returned. The value can be set to at most 1,000, that is, returning up to 1,000 objects in a response. |
|prefix |Query |String |No |abc |Lists objects with a matching prefix. |
|start\-after |Query |String |No |test.txt |Specifies where to start listing. |
|fetch\-owner |Query |Bool |No |false |Specifies whether to return object owner information. Valid values:<br><br><br>* `true`: Return object owner information.<br><br>* `false`: Do not return object owner information. This is the default value. |
|continuation\-token |Query |String |No |whvFnl2rE5vm9cWvQScxwTuNm0\*\*\* |Instructs the listing operation to start from the specified token, which is typically carried over from the `NextContinuationToken` value in the previous response. |


<span id="db4a3e09"></span>
## **Request body elements**

No elements are used.

<span id="b77f35f7"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="bedcd766"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Name |String |Bucket name. |
|Prefix |String |The `prefix` parameter in the request. |
|Marker |String |The `marker` parameter in the request. |
|MaxKeys |Integer |The `max-keys` parameter in the request. |
|Delimiter |String |The `delimiter` parameter in the request. |
|EncodingType |String |The `encoding-type` parameter in the request. |
|IsTruncated |Bool |Whether the returned list is truncated. Valid values:<br><br><br>* `false`: All results have been returned.<br><br>* `true`: Some results are yet to be returned. |
|StartAfter |String |If the request specifies a `StartAfter` parameter, it will also be included in the response. |
|ContinuationToken |String |If the request specifies a `ContinuationToken` parameter, it will also be included in the response. |
|NextContinuationToken |String |When `IsTruncated` is `true`, `NextContinuationToken` is returned, indicating that more entries can be listed. You can include the `NextContinuationToken` value in your next request to continue listing.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of <code>NextContinuationToken</code> is not a real object name.</div><br> |
|CommonPrefixes |Array |If the request specifies a `delimiter`, the response will contain the `CommonPrefixes` element,which summarizes object keys that have the same substring between the prefix and the next occurrence of the `delimiter` into respective groups. |
|Contents |Array |Lists the object information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Contents</code> is the root node for <code>Key</code>, <code>LastModified</code>, <code>ETag</code>, <code>Size</code>, <code>StorageClass</code>, <code>HashCrc64ecma</code>, and <code>Owner</code>.</div><br> |
|Key |String |Object name. |
|LastModified |String |Last modified time of the object. |
|ETag |String |A tag generated at object creation to uniquely identify the object. |
|Size |Integer |Object size. |
|StorageClass |String |Storage type of the object. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive. |
|Type |String |This header is returned for non\-Normal objects. Valid value:<br><br><br>* `Appendable`: The object is uploaded using the AppendObject API.<br><br>* `Symlink`: This object is a symbolic link object. |
|HashCrc64ecma |String |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response.</div><br> |
|Owner |Object |Lists the object owner information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Owner</code> is the root node for <code>ID</code> and <code>DisplayName</code>.</div><br> |
|ID |String |Account ID. |
|DisplayName |String |Display name of the account. |


<span id="6111475a"></span>
## **Sample request**

```JSON
GET /?list-type=2 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id="9d778b38"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: dc13a2093d620014-a444ed0
x-tos-request-id: dc13a2093d620014-a444ed0
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 622

{
    "Name": "bucketName",
    "Prefix": "",
    "Marker": "",
    "MaxKeys": 1000,
    "IsTruncated": false,
    "Contents": [
        {
            "Key": "obj1",
            "LastModified": "2021-08-20T03:10:02.000Z",
            "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
            "Size": 109,
            "StorageClass": "STANDARD"
        },
        {
            "Key": "obj2",
            "LastModified": "2021-08-20T03:10:06.000Z",
            "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
            "Size": 109,
            "StorageClass": "STANDARD"
        },
        {
            "Key": "obj3",
            "LastModified": "2021-08-20T03:10:10.000Z",
            "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
            "Size": 109,
            "StorageClass": "STANDARD"
        }
    ]
}
```
