---
title: "UpdateSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateSourceCode"
---

This interface is used to update the code of a function.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=UpdateSourceCode&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>UpdateSourceCode<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want to update the code.<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>SourceCode<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>Code content. The input requirements are as follows：<br><br>  <br><br> <br> <br><br>* Not empty.<br><br><br> <br> <br><br>* Value after base64 encoding.<br><br><br>  <br><br>  |  <br><br>LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAoKQHJldHVybiAqLwphc3luYyBmdW5jdGlvbiBoYW5kbGVSZXF1ZXN0KHJlcXVlc3QpIHsKICByZXR1cm4gbmV3IFJlc3BvbnNlKCdIZWxsbyBXb3JsZCEnLCB7IHN0YXR1czogMjAwIH0pOwp9Cg==<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=UpdateSourceCode&Version=2021-03-01

{
    "FunctionId":"3gyz993****",
    "SourceCode": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAogKi8KYXN5bmMgZnVuY3Rpb24gaGFuZGxlUmVxdWVzdChyZXF1ZXN0KSB7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="
}
```
