---
title: "ModifyObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Modifyobject"
---

<span id="b07e3974"></span>
## Description

This interface is similar to AppendObject for regular buckets but only supports appending from the end of an object and does not support creating objects through ModifyObject. Moreover, ModifyObject does not differentiate between object types; both regular objects and multipart upload objects support appending.

<span id="J2v89VDP"></span>
## Instructions for Use


* This interface is currently only supported in hierarchical directory buckets.

* Modifications are only supported from the end position of the object.

* Each append upload can be up to 5GiB, and the object size after appending must not exceed 48.8TiB.

* The ModifyObject interface does not support server\-side encryption.

* It is recommended not to perform Modify operations concurrently, as this may lead to execution failures.

* Creating objects through ModifyObject is not supported.

* Modified write does not support chunk mode data upload.

* After a successful modified write, the HeadObject and GetObject response headers' Etag changes to the object's 64\-bit CRC value.

* Modified write is not supported on directories.


<span id="IKDFiPO0"></span>
## **Request syntax**

```JSON
POST /objectName?modify&offset=Offset HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date 
Authorization: authorization string 

<modify data>
```


<span id="iJRkkIcm"></span>
## **Request parameters and headers**

This request uses the public request header, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|modify |Query |String |Yes |\- |Represents a special identifier for the ModifyObject request. |
|offset |Query |Integer |Yes |0 |Specifies where to append from. After a successful append, the response message's x\-tos\-next\-modify\-offset header field will include the offset for the next append. |
|x\-tos\-traffic\-limit |Header |String |No |819200 |TOS provides a single link speed limit feature, controlling the flow in operations like file upload and download to ensure other applications' bandwidth. Value explanations are as follows:<br><br><br>* Value range: 245760\-838860800, unit in bits per second<br><br>* This parameter cannot exist in both Header and Query at the same time |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS provides a single link speed limiting feature, which controls the flow in operations such as uploading and downloading files, to ensure the network bandwidth for other applications. Value explanations are as follows:<br><br><br>* Value range: 245760\-838860800, unit in bits per second<br><br>* This parameter cannot exist simultaneously in both Header and Query |


<span id="FdWH539k"></span>
## **Request body elements**

This request does not contain request message elements; the body carries the data content for modifying and writing objects.

<span id="dGU0XtL0"></span>
## **Response headers**

This request returns the common response message headers, please see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-next\-modify\-offset |Integer |Offset for the next append operation to the object. |
|x\-tos\-hash\-crc64ecma |Integer |Represents the 64\-bit CRC value of the object. The 64\-bit CRC is calculated according to the ECMA\-182 standard. |


<span id="AOx75CQo"></span>
## **Response body elements**

There is no message element in this request response.

<span id="EzfdXcsv"></span>
## **Sample request**

```JSON
POST /objectName?modify&offset=0 HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT 
Authorization: authorization string
```


<span id="EJDvZkUV"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK 
x-tos-id-2: 5726ce090a2d002d-a444ed0 
x-tos-request-id: 5726ce090a2d002d-a444ed0 
Date: Thu, 20 Jun 2024 07:59:37 GMT 
server: TosServer 
Content-Length: 0 
x-tos-next-modify-offset: 4379329 
x-tos-hash-crc64ecma: 6186290338114851376 
ETag: "96e79218965eb72c92a549dd5a330112"
```
