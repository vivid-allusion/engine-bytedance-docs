---
title: "GetBucketHttpsConfig"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbuckethttpsconfig"
---

<span id="cf28eb69"></span>
## Feature description

This interface is used to view the TLS version.

<span id="38bd11d2"></span>
## Request syntax

```JSON
GET /?httpsConfig HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="66bc7d60"></span>
## Request parameters and headers

This request uses common request headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|httpsConfig |Query |String |Yes |\- |Represents a special identifier for the GetBucketHttpsConfig request. |


<span id="d888f3c7"></span>
## Request body elements

This request does not require message elements.

<span id="5bfb159b"></span>
## Response headers

This request returns common response headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="8ca54cd2"></span>
## Response body elements


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TLS |Object |\- |TLS version rules. |
|Enable |Boolean |true |Status of the TLS version setting function, with values explained as follows:<br><br><br>* `true`: enabled<br><br>* `false`: disabled |
|MinTLSVersion |String |TLSv1.0 |Minimum TLS version. |
|MaxTLSVersion |String |TLSv1.2 |Maximum TLS version. |


<span id="b700266d"></span>
## Sample request

```JSON
GET /?httpsConfig HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 +0000
Authorization: authorization string
```


<span id="697ea781"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
{
    "TLS": {
        "Enable": true,
        "MinTLSVersion": "TLSv1.0",
        "MaxTLSVersion": "TLSv1.2"
    }
}
```
