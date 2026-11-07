---
title: "ListSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-Listsparrow"
---

This interface is used to get a list of all functions under the account.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListSparrow&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListSparrow<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |
|  <br><br>OrderType<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The available sorting types are:<br><br>  <br><br> <br> <br><br>* create_time(default): Sort the data based on the time of creation.<br><br><br> <br> <br><br>* update_time: Sort the data based on the time of the last update.<br><br><br>  <br><br>  |  <br><br>create_time<br><br>  |
|  <br><br>Status<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The status of the function.<br><br>  <br><br> <br> <br><br>* 100: running<br><br><br> <br> <br><br>* 400: unassociated<br><br><br> <br> <br><br>* 500: configuring<br><br><br>  <br><br>  |  <br><br>100<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Sparrows<br><br>  |  <br><br>[]Sparrow<br><br>  |  <br><br>See the explanation below.<br><br>  |  <br><br>Function list<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total number of functions<br><br>  |  <br><br>1<br><br>  |

**Sparrow**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>AccountIdentity<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Account ID<br><br>  |  <br><br>20\*\*\*\*<br><br>  |
|  <br><br>Creator<br><br>  |  <br><br>String<br><br>  |  <br><br>Creator<br><br>  |  <br><br>zhangsan<br><br>  |
|  <br><br>Domain<br><br>  |  <br><br>[]String<br><br>  |  <br><br>The domain name bound to the function.<br><br>  |  <br><br>[test\-sparrow.test.test]<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>The ID of the function.<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Name<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of the function.<br><br>  |  <br><br>hello\-ve<br><br>  |
|  <br><br>ProjectName<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of the project to which the function belongs.<br><br>  |  <br><br>default<br><br>  |
|  <br><br>Remark<br><br>  |  <br><br>String<br><br>  |  <br><br>The remark for this function.<br><br>  |  <br><br>this is a test<br><br>  |
|  <br><br>Status<br><br>  |  <br><br>Int32<br><br>  |  <br><br>The status of the function.<br><br>  <br><br> <br> <br><br>* 100: running<br><br><br> <br> <br><br>* 400: unassociated<br><br><br> <br> <br><br>* 500: configuring<br><br><br>  <br><br>  |  <br><br>100<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The creation time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The update time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UserIdentity<br><br>  |  <br><br>Int64<br><br>  |  <br><br>User ID<br><br>  |  <br><br>0\*\*\*\*<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListSparrow&Version=2021-03-01
```

### Sample Response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2021120720555001022524308105******",
    "Action": "ListSparrow",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
     "Sparrows": [
            {
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
        ],
        "TotalCount": 1
  }
}
```
