---
title: "GetSnapshot"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetSnapshot"
---

This interface is used to retrieve detailed information about the code based on the function id and code version.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=GetSnapshot&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>GetSnapshot<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function id<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>VersionTag<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Specify the version tag of the function code you want to view. You can get the version tag by calling the[ListVersions](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListVersions)<br><br> interface.<br><br>  |  <br><br>1.0.1<br><br>  |

### Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>SourceCode<br><br>  |  <br><br>String (ScriptItem)<br><br>  |  <br><br>Function code<br><br>  |  <br><br>See the explanation below<br><br>  |
|  <br><br>Config<br><br>  |  <br><br>String (ConfigItem)<br><br>  |  <br><br>Function configuration<br><br>  |  <br><br>See the explanation below<br><br>  |

**ScriptItem**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>ScriptType<br><br>  |  <br><br>String<br><br>  |  <br><br>Script type<br><br>  |  <br><br>js<br><br>  |
|  <br><br>Source<br><br>  |  <br><br>String<br><br>  |  <br><br>Code content. The code is transformed into a Base64\-encoded format.<br><br>  |  <br><br>See the response example<br><br>  |

**ConfigItem**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Config<br><br>  |  <br><br>map[string]interface{}<br><br>  |  <br><br>Function configuration<br><br>  |  <br><br>See the response example<br><br>  |

### Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetSnapshot&Version=2021-03-01
&FunctionId=3gyz993****
&VersionTag=1.0.1
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022021014244901022524313903*****",
        "Action": "GetSnapshot",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "SourceCode": "{\"script_type\":\"js\",\"source\":\"LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAogKi8KYXN5bmMgZnVuY3Rpb24gaGFuZGxlUmVxdWVzdChyZXF1ZXN0KSB7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ==\"}",
        "Config": "{\"config\":{\"env\":{\"js\":{\"default\":{\"eeee\":\"eee\",\"qqq\":\"qqq\"}}}}}"
    }
}
```
