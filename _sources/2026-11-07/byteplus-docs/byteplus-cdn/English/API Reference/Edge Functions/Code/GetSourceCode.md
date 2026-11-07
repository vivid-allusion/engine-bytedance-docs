---
title: "GetSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetSourceCode-en"
---

Gets the function code. This API returns the code of the `default` script file.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetSourceCode&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `GetSourceCode`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|SourceCode |String |Code content. The code will be converted to Base64 encoding format. |`"LyoqCiAqIEFkZCB0a******uIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="` |
|WasmSourceCode |String |Content of the .wasm file encoded in Base64 format. This parameter is returned only for an OPA function. |`"AGFzbQEAAAABBwFgAn9/AX8DAgEABAUBcAEBAQUDAQAQBhkDfwFBgIDAAAt/AEGAgMAAC38AQYCAwAALBysEBm1lbW9yeQIAA2FkZAAACl9fZGF0YV9lbmQDAQtfX2hlYXBfYmFzZQMCCgkBBwAgASAAagsALwRuYW1lAAw*****3JlZmVyZW5jZS10eXBlcysIc2lnbi1leHQ="` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetSourceCode&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202112072138180102251100110****",
        "Action": "GetSourceCode",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "SourceCode": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAogKi8KYXN5bmMgZnVuY3Rpb24gaGFuZGxlUmVxdWVzdChyZXF1ZXN0KSB7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="
    }
}
```
