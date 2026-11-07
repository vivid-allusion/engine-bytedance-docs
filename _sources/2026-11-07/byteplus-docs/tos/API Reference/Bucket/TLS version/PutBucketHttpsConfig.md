---
title: "PutBucketHttpsConfig"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbuckethttpsconfig"
---

<span id="cf28eb69"></span>
## Feature description

This interface enables or disables the TLS version setting feature.

<span id="38bd11d2"></span>
## Request syntax

```JSON
PUT /?httpsConfig HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
<Optional Additional Header>

{
    "TLS": {
        "Enable": true,
        "MinTLSVersion": "TLSv1.0",
        "MaxTLSVersion": "TLSv1.2"
    }
}
```


<span id="66bc7d60"></span>
## Request parameters and headers

This request uses common request headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|httpsConfig |Query |String |Yes |\- |Special identifier representing the PutBucketHttpsConfig request. |


<span id="8a93a09e"></span>
## Request body elements


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TLS |Object |Yes |\- |TLS version rules. |
|Enable |Boolean |Yes |true |Enable TLS version setting, with the following options:<br><br><br>* `true`: Enable TLS version setting.<br><br>* `false`: Disable TLS version setting. |
|MinTLSVersion |String |No, required when TLS version setting is enabled |TLSv1.0 |Minimum TLS version, with values `TLSv1.0`, `TLSv1.1`, `TLSv1.2`, and `TLSv1.3`. |
|MaxTLSVersion |String |No, required when TLS version is enabled |TLSv1.2 |Maximum TLS version, options are `TLSv1.0`, `TLSv1.1`, `TLSv1.2`, and `TLSv1.3`. |


<span id="d888f3c7"></span>
## Response headers

This request returns common response headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="1b07b690"></span>
## Response body elements

No message elements in this response.

<span id="f97770bd"></span>
## Sample request

```JSON
PUT /?httpsConfig HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
<Optional Additional Header>

{
    "TLS": {
        "Enable": true,
        "MinTLSVersion": "TLSv1.0",
        "MaxTLSVersion": "TLSv1.2"
    }
}
```


<span id="d6e0b462"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
