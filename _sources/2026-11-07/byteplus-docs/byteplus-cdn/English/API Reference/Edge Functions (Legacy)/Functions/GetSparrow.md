---
title: "GetSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetSparrow"
---

This interface is used to get detailed information about a function based on its ID.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=GetSparrow&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>GetSparrow<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the ID of the function for which you want to get details. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow)<br><br> .<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>AccountIdentity<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Account id<br><br>  |  <br><br>20\*\*\*\*<br><br>  |
|  <br><br>Creator<br><br>  |  <br><br>String<br><br>  |  <br><br>Creator<br><br>  |  <br><br>zhangsan<br><br>  |
|  <br><br>Domain<br><br>  |  <br><br>[]String<br><br>  |  <br><br>The domain name bound to the function.<br><br>  |  <br><br>[test\-sparrow.test.test]<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>The ID of the function.<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Name<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of the function.<br><br>  |  <br><br>hello\-ve<br><br>  |
|  <br><br>ProjectName<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of the project to which the function belongs.<br><br>  |  <br><br>default<br><br>  |
|  <br><br>Remark<br><br>  |  <br><br>String<br><br>  |  <br><br>The remark for this function.<br><br>  |  <br><br>this is a test<br><br>  |
|  <br><br>Status<br><br>  |  <br><br>Int32<br><br>  |  <br><br>The status of the function.<br><br>  <br><br> <br> <br><br>* 100: running<br><br><br> <br> <br><br>* 400: unassociated<br><br><br> <br> <br><br>* 500: configuring<br><br><br>  <br><br>  |  <br><br>100<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The creation time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The update time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UserIdentity<br><br>  |  <br><br>Int64<br><br>  |  <br><br>User id<br><br>  |  <br><br>0\*\*\*\*<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetSparrow&Version=2021-03-01
&FunctionId=3gyz993****
```

### Sample Response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2023050920020063355B94DB6C32617243",
    "Action": "GetSparrow",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
     "Sparrow": {
             "AccountIdentity": 20****,
                "CreateTime": 1638326159,
                "Creator": "zhangsan",
                "Domain": [
                    "test-sparrow.test.test"
                ],
                "FunctionId": "3gyz993****",
                "Name": "hello-ve",
                "ProjectName": "default",
                "Remark": "this is a test",
                "Status": 100,
                "UpdateTime": 1638326159,
                "UserIdentity": 0****
        }
  }
}
```
