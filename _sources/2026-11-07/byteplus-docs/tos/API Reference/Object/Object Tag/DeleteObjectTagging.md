---
title: "DeleteObjectTagging"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-deleteobjecttagging"
---

<span id="a976f078"></span>
## **Description**

This API is used to delete tags from an object.

<span id="be418d68"></span>
## **Versioning**

If your bucket has versioning enabled, note the following restrictions when using DeleteObjectTagging:


* By default, the API deletes tags from the current version of the object. Use the `versionId` parameter to specify the target version of action.

* You cannot delete tags from a delete marker if that is what the request URL resolves to. If you try to do so, TOS returns `404 Not Found`.


<span id="48764bb2"></span>
## **Request syntax**

```JSON
DELETE /objectname?tagging
Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue
```


<span id="222ca140"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|tagging |Query |String |Yes |/ |Identifies a DeleteObjectTagging request. |
|versionId |Query |String |No |578946D81EB06437B793 |Version ID of the object, which is used to delete tags from a specific version of the object. |


<span id="a9f566e4"></span>
## **Request body elements**

No elements are used.

<span id="1c2adc2b"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="6f515d7f"></span>
## **Response body elements**

No elements are used.

<span id="ed304770"></span>
## **Sample request**


* Deleting tags from an object

   ```JSON
   DELETE /objectname?tagging
   Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
   Date: Mon, 18 Mar 2019 08:25:17 GMT
   Authorization: SignatureValue
   ```
   

* Deleting tags from a specific version of an object

   ```JSON
   DELETE /objectname?tagging&versionId=***
   Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
   Date: Mon, 18 Mar 2019 08:25:17 GMT
   Authorization: SignatureValue
   ```
   


<span id="3e923de2"></span>
## Sample **response**


* Sample response to deleting tags from an object

   ```JSON
   HTTP/1.1 200 OK
   server: TosServer
   date: Wed, 24 Jun 2020 08:58:15 GMT
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   json
   ```
   

* Sample response to deleting tags from a specific version of an object

   ```JSON
   HTTP/1.1 200 OK
   server: TosServer
   date: Wed, 24 Jun 2020 08:58:15 GMT
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   x-tos-version-id: 578946D81EB06437B793
   json
   ```
