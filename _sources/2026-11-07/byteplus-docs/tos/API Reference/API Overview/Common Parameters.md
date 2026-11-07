---
title: "Common Parameters"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-common-parameters"
---

This topic describes common request and response headers.

<span id="93d1a70b"></span>
## **Common request headers**


|**Header** |**Description** |
|---|---|
|Authorization |Verifies the validity of the request. |
|Content\-Length |The length of the request content (excluding the headers) as defined in RFC 2616. |
|Content\-Type |The request content type. |
|Date |The ISO 8601 UTC timestamp when the request was initiated, in the format of YYYYMMDD'T'HHMMSS'Z'. |
|Host |The requested domain. |


<span id="7adcc3d0"></span>
## **Common response headers**


|**Header** |**Description** |
|---|---|
|Content\-Length |The response body length. |
|Date |The date of the request response, in GMT time. |
|Server |The server that responds to the request. |
|ETag |A piece of information generated during object creation to uniquely identify its content.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">ETag is currently not returned for appendable objects.</div><br> |
|x\-tos\-request\-id |The response ID that uniquely identifies the request. If you encounter a problem while using TOS, contact the TOS support with this field to quickly locate the problem. |
|x\-tos\-id\-2 |A special symbol for problem locating. |
|x\-tos\-server\-time |The time for request processing at the server. |
