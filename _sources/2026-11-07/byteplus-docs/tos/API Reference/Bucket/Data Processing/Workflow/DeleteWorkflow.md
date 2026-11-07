---
title: "DeleteWorkflow"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteWorkflow"
---

<span id="bca5385d"></span>
## Description

This interface deletes a workflow.

<span id="adcf553b"></span>
## Notes

None.

<span id="06ddb6e9"></span>
## Request syntax

```Plain
DELETE /?workflow HTTP/1.1
Host: bucket name.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="2033c221"></span>
## Request parameters and headers 


|**Field name** |**Location **  |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|workflow |Query |String |Yes |\- |Special identifier representing the DeleteWorkflow request. |


<span id="94917cd6"></span>
## **Request body elements**

No elements are used.

<span id="423c4eac"></span>
## **Response headers**

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="2d4a5642"></span>
## **Response body elements**

No elements are used.

<span id="8337cfb5"></span>
## Sample request

```Plain
DELETE /?workflow HTTP/1.1
Host: bucket name.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="79f08947"></span>
## Sample response

```Plain
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
