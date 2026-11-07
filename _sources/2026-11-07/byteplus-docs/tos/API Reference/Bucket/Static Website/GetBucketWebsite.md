---
title: "GetBucketWebsite"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketwebsite"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Description

This interface retrieves the website configuration of the specified bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

You must be the bucket owner or have GetBucketWebsite permission authorized for the current bucket to call this interface.

<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers; see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|website |Query |String |Yes |\- |Special identifier representing the GetBucketWebsite request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used in this request.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

The public response headers returned by this request. See [Public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

<span id=".6YeN5a6a5ZCR5omA5pyJ6K-35rGC"></span>
### Redirect all requests


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|RedirectAllRequestsTo |Object |\- |Redirect all requests; once set, no other redirect rules can be configured. |
|HostName |String |example.com |Redirected site name.<br><br>Parent node: RedirectAllRequestsTo |
|Protocol |String |http |The protocol used for the redirect request, supporting http and https protocols. Defaults to using the http protocol.<br><br>Parent node: RedirectAllRequestsTo |


<span id=".6YeN5a6a5ZCR6KeE5YiZ"></span>
### Redirect rules


* Default homepage IndexDocument



|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|IndexDocument |Object |\- |Set default homepage. |
|Suffix |String |index.html |When requesting a directory (ending with `/`), return objects with the specified `Suffix` under that directory. For example, if `Suffix` is set to `index.html`, accessing `document/` returns `document/index.html`.<br><br>Parent node: IndexDocument |
|ForbiddenSubDir |Bool |false |Whether to support redirecting to the default homepage of a subdirectory; the description is as follows:<br><br><br>* `false` (Default): Does not support redirecting to the default homepage of a subdirectory.<br><br>* `true`: Supports redirecting to the default homepage of a subdirectory.<br><br><br>Parent node: IndexDocument |



* Error page ErrorDocument



|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|ErrorDocument |Object |\- |Set the error page. |
|Key |String |error.html |Return this page when a 4xx error occurs.<br><br>Parent node: ErrorDocument |



* Redirect rules RoutingRules



|**Name** |**Type** |**Example value** |**Note** |
|---|---|---|---|
|RoutingRules |Array |\- |Set the redirect rule. |
|Condition |Object |\- |Set matching conditions for redirect rules. The redirect rule takes effect only when all set conditions match.<br><br>Parent node: RoutingRules |
|HttpErrorCodeReturnedEquals |Integer |404 |Sets the HTTP error code that triggers the redirect. For example, if `HttpErrorCodeReturnedEquals` is set to 404, the rule takes effect when the specified object does not exist.<br><br>If `KeyPrefixEquals` is set, the redirect rule applies only when both conditions match.<br><br>Parent node: Condition |
|KeyPrefixEquals |String |red/ |Set the object name prefix when the redirect rule takes effect.<br><br>If `HttpErrorCodeReturnedEquals` is set, the redirect rule only applies when both conditions match.<br><br>Parent node: Condition |
|Redirect |Object |\- |Set redirection rules.<br><br>Parent node: RoutingRules |
|HostName |String |example.com |Set the site name for redirection.<br><br>Parent node: Redirect |
|HttpRedirectCode |Integer |301 |The status code returned during redirection can only be a 3XX error code, excluding 300. The default is 301.<br><br>Parent node: Redirect |
|Protocol |String |http |The protocol used for redirection requests, supporting http and https. http protocol is used by default.<br><br>Parent node: Redirect |
|ReplaceKeyPrefixWith |String |redirect/ |Object name prefix used for redirection.<br><br>Cannot be set simultaneously with `ReplaceKeyWith`.<br><br>Parent node: Redirect |
|ReplaceKeyWith |String |redirect.html |Object name used during redirection.<br><br>Cannot be set simultaneously with `ReplaceKeyPrefixWith`.<br><br>Parent node: Redirect |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
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
    "IndexDocument": {
        "Suffix": "index.html"
    },
    "ErrorDocument": {
        "Key": "error.html"
    }
}
```
