---
title: "DeleteMultiObjects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-deletemultiobjects"
---

<span id="76e3e7b0"></span>
## **Description**

This API is used to batch delete objects from a bucket. Up to 1,000 objects can be deleted at a time.

If you call this API to batch delete objects from a versioning\-enabled bucket without specifying the `versionId` of an object, TOS will add a delete marker to that object. If a `versionId` is provided, TOS will permanently delete the specified version of that object.

Set the response mode of this API through the `quiet` property. When `quiet` is set to `false`, the deletion result of each object is included in the response regardless of whether the action is successful or not. When `quiet` is set to `true`, only the results of failed deletions are returned, and the absence of a response indicates successful deletion.

<span id="9c2ac897"></span>
## **Request syntax**

```JSON
POST /?delete HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com 
Date: GMT Date
Authorization: authorization string
Content-MD5: md5 string

{
  "Objects": [{
    "Key": "obj1"
    "VersionId": "string"
  }],
  "Quiet": false
}
```


<span id="6d97c93e"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|delete |Query |String |Yes | |Identifies a DeleteMultipleObjects request. |
|Content\-MD5 |Header |String |Yes |dgWRtDmbPCHa/IS1s7XxUg== |Resulting string from MD5 calculation and Base64 encoding of the request body. |


<span id="32fd0b77"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Objects |Array |Yes |\- |Root node for the list of objects to delete. |
|Key |String |Yes |objectName |Name of the object to delete. Parent node: Objects. |
|VersionId |String |No |57AF1A32CECB56721267 |ID of the object version to delete. Parent node: Objects. |
|Quiet |Bool |No |false |Response mode after batch deletion. Valid values:<br><br><br>* `false`: Returns all deletion results in the response body. This is the default value.<br><br>* `true:` Returns only the failed deletions. |


<span id="561bfc03"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="b8226224"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Deleted |Array |List of successful deletions. |
|Key |String |Name of the deleted object. |
|DeleteMarker |Bool |Identifies a delete marker. |
|DeleteMarkerVersionId |String |Version ID of the delete marker. |
|Error |Object |List of failed deletions. |
|Code |String |Error code of the failed deletion. |
|Message |String |Error message of the failed deletion. |


<span id="28b680a3"></span>
## **Sample request 1**

```JSON
POST /?delete HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com 
Date: Fri, 30 Jul 2021 13:56:19 GMT
Authorization: authorization string
Content-MD5: md5 string

{
  "Objects": [{
    "Key": "obj1"
  },
  {
    "Key": "obj2"
  }],
  "Quiet": false
}
```


<span id="c314c036"></span>
## **Sample response 1**

A success response:

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:56:19 GMT
Server: TosServer
Content-Type: application/xml
x-tos-id-2: 4fac130bee03002e-a444ed0
x-tos-request-id: 4fac130bee03002e-a444ed0

{
    "Deleted": [
        {
            "Key": "obj2"
        },
        {
            "Key": "obj1"
        }
    ]
}
```


A failure response:

```JSON
HTTP/1.1 400 Bad Request
Date: Fri, 30 Jul 2021 13:56:52 GMT
Server: TosServer
x-tos-id-2: 4fac130bee240030-a444ed0
x-tos-request-id: 4fac130bee240030-a444ed0

{
    "Code": "BadDigest",
    "RequestId": "4d31430787b94d11b80b348122ff2290-ac1a1791",
    "HostId": "GFdpcBKxovJAtAdAQluzipAXqaRyDTc",
    "Message": "The Content-MD5 you specified did not match what we received."
}
```


<span id="8894c2d3"></span>
## **Sample request 2**

This request deletes an object from a versioning\-enabled bucket. As the versionId is not specified, TOS fulfills the request by adding a delete marker.

```JSON
POST /?delete HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com 
Date: Fri, 30 Jul 2021 13:56:19 GMT
Authorization: authorization string
Content-MD5: md5 string

{
  "Objects": [{
    "Key": "obj1"
  }],
  "Quiet": false
}
```


<span id="50a23ba9"></span>
## **Sample response 2**

A success response in the above scenario.

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:56:19 GMT
Server: TosServer
x-tos-id-2: 4fac130bee03002e-a444ed0
x-tos-request-id: 4fac130bee03002e-a444ed0

{
    "Deleted": [
        {
            "Key": "obj1",
            "DeleteMarker": true,
            "DeleteMarkerVersionId": "581CAE50578790BEF9C2"
        }
    ]
}
```


<span id="87b6bf62"></span>
## **Sample request 3**

This request deletes a particular version of an object from a versioning\-enabled bucket by specifying the versionId.

```JSON
POST /?delete HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com 
Date: Fri, 30 Jul 2021 13:56:19 GMT
Authorization: authorization string
Content-MD5: md5 string

{
  "Objects": [{
    "Key": "obj1",
    "VersionId": "581CAE10FC6325DEBC3F"
  }],
  "Quiet": false
}
```


<span id="c2e63cad"></span>
## **Sample response 3**

A success response in the above scenario.

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:56:19 GMT
Server: TosServer
x-tos-id-2: 4fac130bee03002e-a444ed0
x-tos-request-id: 4fac130bee03002e-a444ed0

{
    "Deleted": [
        {
            "Key": "obj1",
            "DeleteMarker": true,
            "DeleteMarkerVersionId": "581CAE10FC6325DEBC3F"
        }
    ]
}
```


<span id="7f19a9c3"></span>
## **Sample request 4**

This request tries to batch delete objects and has resulted in a mix of successful and failed actions. In this example, the requester has no permission to delete obj2.

```JSON
POST /?delete HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com 
Date: Fri, 30 Jul 2021 13:56:19 GMT
Authorization: authorization string
Content-MD5: md5 string

{
  "Objects": [{
    "Key": "obj1"
  },
  {
    "Key": "obj2"
  }],
  "Quiet": false
}
```


<span id="8650ae15"></span>
## **Sample response 4**

The response includes a Deleted array of the successfully deleted objects and an Error array of the failed ones.

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:56:19 GMT
Server: TosServer
x-tos-id-2: 4fac130bee03002e-a444ed0
x-tos-request-id: 4fac130bee03002e-a444ed0

{
    "Deleted": [
        {
            "Key": "obj1"
        }
    ],
    "Error": [
        {
            "Code": "AccessDenied",           
            "Message": "Access Denied",
            "Key": "obj2"
        }
    ]
}
```
