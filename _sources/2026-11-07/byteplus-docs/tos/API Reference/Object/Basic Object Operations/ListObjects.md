---
title: "ListObjects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-listobjects"
---

<span id="36efe39a"></span>
## **Description**

This API is used to list objects in a bucket.

To use it, you must have read access to the bucket. This API returns a maximum of 1,000 objects in the bucket for each request. You can use request parameters to define the selection criteria for the objects to list.

<span id="0e4982bf"></span>
## **Request syntax**

```JSON
GET / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="69ba10e5"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|delimiter |Query |String |No |/ |Specifies the character used to group the object keys,which is usually a forward slash ( / ). |
|encoding\-type |Query |String |No |url |Specifies the encoding of the returned content. Valid value:<br><br><br>* url: Use URL encoding. |
|max\-keys |Query |Integer |No |100 |Specifies the maximum number of objects returned. The value can be set to at most 1,000, that is, returning up to 1,000 objects in a response. |
|prefix |Query |String |No |abc |Lists objects with a matching prefix. |
|marker |Query |String |No |test.txt |Specifies where to start listing. Objects are listed in alphabetical order after the specified start. The value is typically carried over from the NextMarker value in the previous response. |


<span id="86119656"></span>
## **Request body elements**

No elements are used.

<span id="7da44138"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="24e5c471"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Name |String |Bucket name. |
|Prefix |String |The prefix parameter in the request. |
|Marker |String |The marker parameter in the request. |
|MaxKeys |Integer |The max\-keys parameter in the request. |
|Delimiter |String |The delimiter parameter in the request. |
|EncodingType |String |The encoding\-type parameter in the request. |
|IsTruncated |Bool |Whether the returned list is truncated. Valid values:<br><br><br>* false: All results have been returned.<br><br>* true: Some results are yet to be returned. |
|NextMarker |String |Indicates the marker value to use in the next request if some results are yet to be returned. |
|CommonPrefixes |Array |If the request specifies a delimiter, the response will contain the CommonPrefixes element,which summarizes object keys that have the same substring between the prefix and the next occurrence of the delimiter into respective groups. |
|Contents |Array |Root node for object information. |
|Key |String |Object name. Parent node: Contents. |
|LastModified |String |Last modified time of the object. Parent node: Contents. |
|ETag |String |A piece of information generated at object creation to uniquely identify its content. Parent node: Contents. |
|Size |Integer |Object size. Parent node: Contents. |
|StorageClass |String |Storage type of the object. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br><br>Parent node: Contents. |
|Type |String |This header is returned for non\-Normal objects. Valid value:<br><br><br>* `Appendable`: The object is uploaded using the AppendObject API.<br><br>* `Symlink`：This object is a symbolic link object.<br><br><br>Parent node: Contents. |
|HashCrc64ecma |String |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response.</div><br><br><br>Parent node: Contents. |
|Owner |Object |Object owner. Parent node: Contents. |
|ID |String |Account ID. Parent node: Owner. |
|DisplayName |String |Display name of the account. Parent node: Owner. |


<span id="3be1eb89"></span>
## **Sample request**

```JSON
GET / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id="90fa58e4"></span>
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
