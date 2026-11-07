---
title: "GetBucketCORS"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getbucketcors"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface retrieves the current Cross\-Origin Resource Sharing (CORS) configuration rules of the specified bucket.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Your account must have <code>tos:GetBucketCORS</code> permission to obtain the bucket’s CORS rules. For details, see the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?cors HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers; refer to [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|cors |Query |String |Yes |\- |Identifies a GetBucketCORS request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns public response headers. See [Public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

The response contains the complete set of CORS rules of the bucket.


|**Name** |**Type** |**Sample Value** |**Note** |
|---|---|---|---|
|CORSRules |Array |\- |The CORS rule information. |
|AllowedOrigins |Array |["\*"] |Specifies the allowed origins of cross\-origin requests. |
|AllowedMethods |Array |["PUT", "GET"] |Specifies the allowed cross\-origin request methods. |
|AllowedHeaders |Array |["Authorization"] |Specifies the allowed headers. |
|ExposeHeaders |Array |["x\-tos\-test"] |Specifies the allowed response headers. |
|MaxAgeSeconds |Integer |1024 |The maximum cache time. |
|ResponseVary |Bool |false |Whether to return the `Vary: Origin` header. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?cors HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643

{
    "CORSRules":[
        {
            "AllowedOrigins":["http://www.example.com"],
            "AllowedMethods":["PUT", "GET"],
            "AllowedHeaders":["*"],
            "ExposeHeaders":["x-tos-test"],
            "MaxAgeSeconds":1024,
            "ResponseVary" : false
        }
    ]
}
```
