---
title: "PutBucketCORS"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putbucketcors"
---

<span id="9DKgv8Rv"></span>
## Introduction

This interface sets Cross\-Origin Resource Sharing (CORS) rules for a bucket. You can use the `Content-MD5` header to provide the expected MD5 value, which will be compared with the MD5 of the uploaded object; if they do not match, an error will be returned.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you want to set CORS rules for the bucket, your account must have <code>tos:PutBucketCORS</code> permission. For details, see the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">TOS supports setting multiple CORS rules, but the total size of all rules cannot exceed 20KiB.</div>



<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
PUT /?cors HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string

{
    "CORSRules":[
        {
            "AllowedOrigins":["the origin you want allow CORS request from"],
            "AllowedMethods":["HTTP method"],
            "AllowedHeaders":["headers that allowed browser to send"],
            "ExposeHeaders":["headers in response that can access from client app"],
            "MaxAgeSeconds":1024,
            "ResponseVary" : true
        }
    ]
}
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|cors |Query |String |Yes |\- |Identifies a PutBucketCORS request. |
|Content\-MD5 |Header |String |No |XrY7u+Ae7tCTyyK7j1rNww== |Base64\-encoded MD5 digest of the message body. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements


|**Name** |**Type** |**Required** |**Example value** |**Note** |
|---|---|---|---|---|
|CORSRules |Array |Yes |\- |The CORS rule information. |
|AllowedOrigins |Array |Yes |["\*"] |Specify the allowed origins of cross\-origin requests. Constraints:<br><br><br>* List IP addresses or domain names, optionally with port numbers.<br><br>* Must include https:// or http://.<br><br>* Multiple entries are allowed, with one entry per line separated by line breaks.<br><br>* Each line can contain at most one wildcard (`*`). |
|AllowedMethods |Array |Yes |["PUT", "GET"] |Specify the allowed cross\-origin request methods, one or more can be specified, including `PUT`, `GET`, `POST`, `DELETE`, and `HEAD`. |
|AllowedHeaders |Array |No |["Authorization"] |Specifies the allowed cross\-origin request headers. Constraints:<br><br><br>* Multiple entries are allowed, with one entry per line separated by carriage returns.<br><br>* Set to `*` by default unless otherwise required, indicating all are allowed. |
|ExposeHeaders |Array |No |["x\-tos\-request\-id"] |Specify additional headers in CORS responses exposed to clients to provide extra information. Constraints:<br><br><br>* Multiple headers can be specified, one per line, separated by line breaks.<br><br>* Wildcards (`*`) are not allowed.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">It is generally recommended to add the X\-Tos\-Request\-Id and ETag headers.</div><br> |
|MaxAgeSeconds |Integer |No |1024 |Indicates how long the results of an OPTIONS request can be cached, in seconds. The default is 3600. |
|ResponseVary |Bool |No |false |Return `Vary: Origin` header?<br><br><br>* `false`(Default): Does not return `Vary: Origin` header.<br><br>* `true`: Returns `Vary: Origin` header.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Enabling <strong>Return Vary: Origin</strong> may increase the number of visits or CDN back\-to\-origin requests.</div><br> |


<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

The public response headers returned by this request, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

No elements are used.

<span id=".6K-35rGC56S65L6LLTE="></span>
## Sample request 1

Configure a CORS rule for the bucket.

```JSON
PUT /?cors HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string

{
    "CORSRules":[
        {
            "AllowedOrigins":["*"],
            "AllowedMethods":["PUT", "GET"],
            "AllowedHeaders":["Authorization"],
            "ExposeHeaders":["x-tos-request-id"],
            "MaxAgeSeconds":1024
        }
    ]
}
```


<span id=".5ZON5bqU56S65L6LLTE="></span>
## Sample response 1

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```


<span id=".6K-35rGC56S65L6LLTI="></span>
## Sample request 2

Configure the bucket to allow cross\-origin PUT and POST requests from `http://www.example.com` and enable the return of the Vary: Origin header. MaxAgeSeconds helps prevent browsers from sending OPTION requests for the same request.

```JSON
PUT /?cors HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string

{
    "CORSRules":[
        {
            "AllowedOrigins":["http://www.example.com"],
            "AllowedMethods":["PUT", "GET"],
            "AllowedHeaders":["*"],
            "ExposeHeaders":["x-tos-request-id"],
            "MaxAgeSeconds":1024,
            "ResponseVary" : true
        }
    ]
}
```


<span id=".5ZON5bqU56S65L6LLTI="></span>
## Sample response 2

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```
