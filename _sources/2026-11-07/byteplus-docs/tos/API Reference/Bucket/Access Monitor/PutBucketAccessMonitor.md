---
title: "PutBucketAccessMonitor"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketAccessMonitor"
---

<span id="e944a894"></span>
## **Description**

This interface is used to set up access monitor for buckets. You must enable access monitor before creating a lifecycle rule for the last access time. Once this feature is enabled, TOS will automatically start checking and recording the last access time of all objects under the bucket.

<span id="caf01e56"></span>
## Precautions


* Enabling access monitor feature will incur monitoring fees, but TOS currently does not charge this fee.

* Before you enable access monitor, you must first delete all lifetime rules for the last access time type, otherwise, it cannot be closed.


<span id="66114ef6"></span>
## **Request syntax**

```Bash
PUT /?accessmonitor HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Status": "Enabled"
}
```


<span id="0daa5272"></span>
## Request parameters and headers

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="d965f745"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Status |Boolean |Yes |Enabled |Whether to enable the access monitor function, the value selection description is as follows:<br><br><br>* `Enabled`: Enable access monitor.<br><br>* `Disabled`: Disable access monitor. |


<span id="35b30a3d"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="a3575324"></span>
## **Response body elements**

There is no message element in the request response.

<span id="14910ce9"></span>
## **Sample request**

```Bash
PUT /?accessmonitor HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Status": "Enabled"
}
```


<span id="ac63d427"></span>
## **Sample response**

```Bash
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```
