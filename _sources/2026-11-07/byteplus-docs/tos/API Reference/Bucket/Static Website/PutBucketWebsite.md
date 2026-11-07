---
title: "PutBucketWebsite"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketwebsite"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

You can use the PutBucketWebsite interface to set the bucket to static website hosting mode and configure redirect rules. This mode supports the following functions:


* Redirect all requests to another site.

* Set specific rules to redirect particular requests.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You must be the bucket owner or have PutBucketWebsite permission for the current bucket to call this interface.

* You can set up to 50 redirect rules.

* You must configure a custom domain before static website hosting mode takes effect.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
PUT /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 120

{
    "RedirectAllRequestsTo": {
        "HostName": "example.com",
        "Protocol": "https"
    },
    "IndexDocument": {
        "Suffix": "index.html",
        "ForbiddenSubDir": "false"
    },
    "ErrorDocument": {
        "Key": "error.html"
    },
    "RoutingRules": [
        {
            "Condition": {
                "HttpErrorCodeReturnedEquals": 404,
                "KeyPrefixEquals": "red/"
            },
            "Redirect": {
                "HostName": "example.com",
                "HttpRedirectCode": 301,
                "Protocol": "http",
                "ReplaceKeyPrefixWith": "redirect/",
                "ReplaceKeyWith": "redirect.html"
            }
        }
    ]
}
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|website |Query |String |Yes |\- |Represents a special identifier for the PutBucketWebsite request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

<span id=".6YeN5a6a5ZCR5omA5pyJ6K-35rGC"></span>
### Redirect all requests


|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|RedirectAllRequestsTo |Object |No |\- |Redirect all requests. Once set, no other redirect rules can be applied. |
|HostName |String |Required if using RedirectAllRequestsTo |example.com |Redirected site name.<br><br>Parent node: RedirectAllRequestsTo |
|Protocol |String |No |http |protocol used for redirect requests, supports http and https protocols. http protocol is used by default.<br><br>parent node: RedirectAllRequestsTo |


<span id=".6YeN5a6a5ZCR6KeE5YiZ"></span>
### Redirect rules


* Default home page IndexDocument



|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|IndexDocument |Object |No |\- |Set the default homepage. |
|Suffix |String |Required if using IndexDocument |index.html |When requesting a directory (ending with`/`), return the `Suffix` object under that directory. For example, if the `Suffix` is set to `index.html`, accessing `document/` will return `document/index.html`.<br><br>Parent node: IndexDocument |
|ForbiddenSubDir |Bool |No |false |whether to support redirecting to the default homepage of the subdirectory. the value descriptions are as follows:<br><br><br>* `false` (default): does not support redirecting to the default homepage of the subdirectory.<br><br>* `true`: supports redirecting to the default homepage of the subdirectory.<br><br><br>parent node: IndexDocument |



* Error page ErrorDocument



|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|ErrorDocument |Object |No |\- |Set the error page. |
|Key |String |If using ErrorDocument, it is required |error.html |If a 4xx error occurs, this page is returned.<br><br>Parent node: ErrorDocument |



* Redirect rules RoutingRules



|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|RoutingRules |Array |No |\- |Set redirect rules. |
|Condition |Object |Required if RoutingRules is used |\- |Set matching conditions for redirect rules. The redirect rules take effect only when all the set conditions match.<br><br>Parent node: RoutingRules |
|HttpErrorCodeReturnedEquals |Integer |No |404 |Set the HTTP error code for redirect activation. For example, set `HttpErrorCodeReturnedEquals` to 404. The rule takes effect when the specified object is not found.<br><br>If `KeyPrefixEquals` is set, both conditions must match for the redirect rule to take effect.<br><br>Parent node: Condition |
|KeyPrefixEquals |String |No |red/ |set the object name prefix when the redirect rule takes effect.<br><br>If `HttpErrorCodeReturnedEquals` is set, the redirect rule works only when both conditions match.<br><br>Parent node: Condition |
|Redirect |Object |If using RoutingRules, it is required |\- |Set redirect rules.<br><br>Parent node: RoutingRules |
|HostName |String |No |example.com |Set the site name for redirection.<br><br>Parent node: Redirect |
|HttpRedirectCode |Integer |No |301 |Status code returned when redirecting; only 3XX error codes can be set, 300 is not allowed, default is 301.<br><br>Parent node: Redirect |
|Protocol |String |No |http |The protocol used for redirect requests; supports http and https protocols. http protocol is used by default.<br><br>Parent node: Redirect |
|ReplaceKeyPrefixWith |String |No |redirect/ |Prefix for the object name used during redirection.<br><br>Cannot be set simultaneously with `ReplaceKeyWith`.<br><br>Parent node: Redirect |
|ReplaceKeyWith |String |No |redirect.html |The object name used during redirection.<br><br>Cannot be set simultaneously with `ReplaceKeyPrefixWith`.<br><br>Parent node: Redirect |


<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns public response headers. See [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

No elements are used in this response.

<span id=".6K-35rGC56S65L6LLTE="></span>
## Sample request 1

```JSON
PUT /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 76

{
    "RedirectAllRequestsTo": {
        "HostName": "example.com"
    }
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
```


<span id=".6K-35rGC56S65L6LLTI="></span>
## Sample request 2

```JSON
PUT /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 122

{
    "IndexDocument": {
        "Suffix": "index.html"
    },
    "ErrorDocument": {
        "Key": "error.html"
    }
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
```
