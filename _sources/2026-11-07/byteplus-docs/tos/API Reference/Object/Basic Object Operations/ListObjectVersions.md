---
title: "ListObjectVersions"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-listobjectversions"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## **Feature description**

This API is used to list multiversion objects in a bucket. To use it, you must have read access to the bucket. This API returns a maximum of 1,000 multiversion objects in the bucket for each request. You can use request parameters to define the selection criteria for the objects to list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">HNS buckets do not support the ListObjectVersions API yet.</div>


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## **Request syntax**

```JSON
GET /?versions HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## **Request parameters and headers**

This request uses the common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|versions |Query |String |Yes |\- |Identifies a ListObjectVersions request. |
|delimiter |Query |String |No |\- |Specifies the character used to group the object keys, which is usually a forward slash ( / ). |
|encoding\-type |Query |String |No |url |Specifies the encoding of the returned content. Valid values are as follows:<br><br><br>* `url`: Perform URL encoding following the application/x\-www\-form\-urlencoded standard. |
|max\-keys |Query |Integer |No |100 |Specifies the maximum number of multiversion objects returned. The value can be set to at most 1,000, that is, returning up to 1,000 multiversion objects in a response. |
|prefix |Query |String |No |aaa |Lists multiversion objects with a matching prefix. |
|key\-marker |Query |String |No |test.txt |Specifies where to start listing. Multiversion objects are listed in alphabetical order after the specified start. The value is typically carried over from the NextKeyMarker value in the previous response. |
|version\-id\-marker |Query |String |No |123 |This parameter is used with key\-marker in multiversion object listing scenarios to indicate to start listing from the specified version in alphabetical order. The version\-id\-marker is invalid if it is not a version associated with the key\-marker. The value is typically carried over from the NextVersionIdMarker value in the previous response. |


<span id=".6K-35rGC5YWD57Sg"></span>
## **Request body elements**

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## **Response headers**

This request returns common response headers; see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Note** |
|---|---|---|---|
|Name |String |test\-bucket |Bucket name. |
|KeyMarker |String |abc |The key\-marker parameter in the request. |
|VersionIdMarker |String |57AF1A32CECB56721267 |The version\-id\-marker parameter in the request. |
|MaxKeys |Integer |100 |The max\-keys parameter in the request. |
|Prefix |String |abc |The prefix parameter in the request. |
|Delimiter |String |d |The delimiter parameter in the request. |
|EncodingType |String |url |The encoding\-type parameter in the request. |
|IsTruncated |Bool |true |Whether the returned list is truncated. Valid values:<br><br><br>* `false`: all results have been returned.<br><br>* `true`: some results have not yet returned. |
|NextKeyMarker |String |abcd |Indicates the key\-marker value to use in the next request if some results are yet to be returned. |
|NextVersionIdMarker |String |26AG6A32CECA56721238 |Indicates the version\-id\-marker value to use in the next request if some results are yet to be returned. |
|CommonPrefixes |Array |[{"Prefix": "abcd"}] |If the request specifies a delimiter, the response will contain the CommonPrefixes element. This element identifies a collection of object names that end with the delimiter and share a common prefix. |
|DeleteMarkers |Array |\- |Root node for delete marker information. |
|Versions |Array |\- |Root node for multiversion object information. |
|Key |String |abcde |Name of the multiversion object or delete marker. Parent node: Versions or DeleteMarkers. |
|LastModified |String |2024\-06\-06T07:15:20.000Z |Last modified time of the object version or delete marker. Parent node: Versions or DeleteMarkers. |
|IsLatest |Bool |true |Whether the version is the latest. Valid values:<br><br><br>* `false`: not the latest version.<br><br>* `true`: the latest version.<br><br><br>Parent node: Versions or DeleteMarkers. |
|VersionId |String |19EA1B32CEEB56721221 |Version ID of the multiversion object or delete marker. Parent node: Versions or DeleteMarkers. |
|ETag |String |"32185e15494ca8e0eedf12bd218787f6" |A piece of information generated at object version creation to uniquely identify its content. Parent node: Versions. |
|Size |Integer |4813 |Size of the object version. Parent node: Versions. |
|StorageClass |String |STANDARD |Storage type of the multiversion object. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage.<br><br>* `ARCHIVE_FR`: Archive Flashback Storage.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br><br>Parent node: Versions. |
|Type |String |Appendable |When the object is not a Normal object, this element is returned. The values are explained as follows:<br><br><br>* `Appendable`: The object is uploaded via the append write interface.<br><br>* `Symlink`: The object is a symbolic link.<br><br><br>Parent node: Versions. |
|HashCrc64ecma |String |2217460101204276403 |CRC\-64 value of the multiversion object, which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response.</div><br><br><br>Parent node: Versions. |
|Owner |Object |\- |Multiversion object owner. Parent node: Versions. |
|ID |String |1234567890 |Account ID. Parent node: Owner. |
|DisplayName |String |test\-owner\-name |Display name of the account. Parent node: Owner. |


<span id=".6K-35rGC56S65L6L"></span>
## **Sample request**

```JSON
GET /?versions HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: dc13a2093af10012-a444ed0
x-tos-request-id: dc13a2093af10012-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 874

{
    "Name": "bucketName",
    "Prefix": "",
    "KeyMarker": "",
    "VersionIdMarker": "",
    "MaxKeys": 1000,
    "IsTruncated": false,
    "Versions": [
        {
            "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
            "IsLatest": true,
            "Key": "obj1",
            "LastModified": "2021-08-20T03:40:54.000Z",
            "Owner": {
                "ID": "AccountID",
                "DisplayName": "DisplayName"
            },
            "Size": 109,
            "StorageClass": "STANDARD",
            "VersionId": "5840E600C6FBD446792D"
        },
        {
            "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
            "IsLatest": false,
            "Key": "obj1",
            "LastModified": "2021-08-20T03:10:02.000Z",
            "Owner": {
                "ID": "AccountID",
                "DisplayName": "DisplayName"
            },
            "Size": 109,
            "StorageClass": "STANDARD",
            "VersionId": "5840E7AFE74C1A18232F"
        }
    ],
    "DeleteMarkers": [
        {
            "IsLatest": false,
            "Key": "obj1",
            "LastModified": "2021-08-20T03:40:22.000Z",
            "Owner": {
                "ID": "AccountID",
                "DisplayName": "DisplayName"
            },
            "VersionId": "5840E60831A5DBABA376"
        }
    ]
}
```
