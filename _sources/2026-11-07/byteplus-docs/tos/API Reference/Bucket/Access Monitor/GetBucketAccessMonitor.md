---
title: "GetBucketAccessMonitor"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketAccessMonitor"
---

<span id="17fa2a6b"></span>
## **Description**

This interface is used to obtain configuration information for access tracing.

<span id="8a64bc7b"></span>
## **Request syntax**

```Bash
GET /?accessmonitor HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="fa2b6045"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|accessmonitor |Query |String |Yes |\- |Special identification representing GetBucketAccessMonitor requests. |


<span id="5e7b3675"></span>
## **Request body elements**

No elements are used.

<span id="d676eec9"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="fb6f337a"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Status |String |Enabled |Whether to enable the access monitor function, the value selection description is as follows:<br><br><br>* `Enabled`: Enable access monitor.<br><br>* `Disabled`: Disable access monitor. |


<span id="00d92173"></span>
## **Sample request**

```Bash
GET /?accessmonitor HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="a3f9e066"></span>
## **Sample response**

```Bash
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
{
    "Status": "Enabled"
}
```
