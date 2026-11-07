---
title: "SetObjectExpires"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/SetObjectExpires"
---

<span id="1b913062"></span>
## Feature description

This interface adds or modifies the expiration time of an object.

<span id="59133263"></span>
## Request syntax

```Bash
POST /ObjectName?objectExpires HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Thu, 28 Aug 2025 09:48:41 GMT
Authorization: authorization string
{   
    "ObjectExpires": 1
}
```


<span id="23cbe966"></span>
## Request parameters and headers

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|objectExpires |Query |String |Yes |\- |Special identifier representing the SetObjectExpires request. |


<span id="c3421638"></span>
## Request body elements


|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|ObjectExpires |Integer |Yes |1 |Add or modify the expiration time of an object. After expiration, TOS automatically deletes the object. The unit is days. The values are described as follows:<br><br><br>* Positive integer: the object expires at the specified time, calculated from the object's Last\-Modified time. Deletion begins at midnight after the expiration time. For example, if the `ObjectExpires` parameter is set to`3`and the object's Last\-Modified time is 2024\-09\-26 12:00, then the object expires at 2024\-09\-30 00:00.<br><br>* 0: Never expires; the object will remain in the bucket until you manually delete it or configure a lifecycle rule to delete it.<br><br>   You can set this parameter value to`0`to make objects with a specified expiration time never expire.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Expiring objects via APIs takes precedence over lifecycle deletion rules. For instance, if an object's expiration time is set to five days and a lifecycle rule specifies deletion after three days, the object will be deleted after five days based on its expiration time.</div><br> |


<span id="9fb4fd2d"></span>
## Response headers

This request returns common response headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="4c803fae"></span>
## Response body elements

No elements are used in this response.

<span id="0b13aa9c"></span>
## Sample request

```Bash
POST /data.txt?objectExpires HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Thu, 28 Aug 2025 09:32:02 +0000
Authorization: authorization string
{   
    "ObjectExpires": 1
}
```


<span id="1fff8fba"></span>
## Sample response

```Bash
HTTP/1.1 204 No Content
Date: Thu, 28 Aug 2025 09:48:41 GMT
Server: TosServer
x-tos-id-2: fb7701b025f994d568b025f9-b8943ad
x-tos-request-id: fb7701b025f994d568b025f9-b8943ad
```
