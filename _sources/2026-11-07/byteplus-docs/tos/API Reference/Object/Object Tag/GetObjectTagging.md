---
title: "GetObjectTagging"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getobjecttagging"
---

<span id="fc6be80e"></span>
## **Description**

This API is used to get the tags of an object.

<span id="6d03695d"></span>
## **Versioning**

If your bucket has versioning enabled, note the following restrictions when using GetObjectTagging:


* By default, the API gets the tags of the current version of the object. Use the `versionId` parameter to specify the target version of action.

* You cannot get tags of a delete marker if that is what the request URL resolves to. If you try to do so, TOS returns `404 Not Found`.


<span id="eb12b636"></span>
## **Request syntax**

```JSON
GET /objectname?tagging
Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue
```


<span id="b48739bb"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|tagging |Query |String |Yes |/ |Identifies a GetObjectTagging request. |
|versionId |Query |String |No |57894830D7822B2ACB78 |Version ID of the object, which is used to get the tags of a specific version of the object. |


<span id="40c23aef"></span>
## **Request body elements**

No elements are used.

<span id="0ec9b191"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="c4ba8ff2"></span>
## **Response body elements**

The response body represents the desired tagging of the object.


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TagSet |Container |/ |A set of tags. |
|Tags |Container |/ |Tag information. |
|Key |String |aa |Tag key. |
|Value |String |bb |Tag value. |


<span id="8343bc9f"></span>
## **Sample request**


* Getting tags of an object

   ```JSON
   GET /objectname?tagging
   Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
   Date: Mon, 18 Mar 2019 08:25:17 GMT
   Authorization: SignatureValue
   ```
   

* Getting tags of a specific version of an object

   ```JSON
   PUT /objectname?tagging&versionId=***
   Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
   Date: Mon, 18 Mar 2019 08:25:17 GMT
   Authorization: SignatureValue
   ```
   


<span id="12007fd6"></span>
## Sample **response**


* Sample response to getting tags of an object

   ```JSON
   HTTP/1.1 200 OK
   date: Wed, 24 Jun 2020 08:57:15 GMT
   content-length: 142
   server: TosServer
   x-tos-id-2: 4fac130bedb6002c-a444ed0
   x-tos-request-id: 4fac130bee03002e-a444ed0
   {"TagSet": {"Tags": [{"Key": "dd", 
                   "Value": "ee"},{"Key": "bb", 
                   "Value": "cc"}]}}
   json
   ```
   

* Sample response to getting tags of a specific version of an object

   ```JSON
   HTTP/1.1 200 OK
   date: Wed, 24 Jun 2020 08:58:15 GMT
   content-length: 142
   server: TosServer
   x-tos-id-2: ea2ceb08a4e30021-a444ed0
   x-tos-request-id: 5726ce090a2d002d-a444ed0
   x-tos-version-id: 57894830D7822B2ACB78
   {"TagSet": {"Tags": [{"Key": "aa", 
                   "Value": "bb"},{"Key": "bb", 
                   "Value": "cc"}]}}
   ```
