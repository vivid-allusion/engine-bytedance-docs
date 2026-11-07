---
title: "GetScriptSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetScriptSourceCode"
---

This interface is used to get the code of all script files in the function based on the function id.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=GetScriptSourceCode&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>GetScriptSourceCode<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function id<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |

### Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>ScriptSourceCode<br><br>  |  <br><br>map<br><br>  |  <br><br>Function code<br><br>  |  <br><br>See the explanation below.<br><br>  |

#### ScriptSourceCode

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>_key<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of script file.<br><br>  |  <br><br>See the explanation below.<br><br>  |
|  <br><br>_value<br><br>  |  <br><br>String<br><br>  |  <br><br>The code content of script file. The code is transformed into a Base64\-encoded format.<br><br>  |  <br><br>See the explanation below.<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetScriptSourceCode&Version=2021-03-01
&FunctionId=3gyz993****
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022021014244901022524313903*****",
        "Action": "GetScriptSourceCode",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ScriptSourceCode": {
            "test": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAoKQHJldHVybiAqLwphc3luYyBmdW5jdGlvbiBoYW5kbGVSZXF1ZXN0KHJlcXVlc3QpIHsKICByZXR1cm4gbmV3IFJlc3BvbnNlKCdIZWxsbyBXb3JsZCEnLCB7IHN0YXR1czogMjAwIH0pOwp9Cg=="
        }
    }
}
```
