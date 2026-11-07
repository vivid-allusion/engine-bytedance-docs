---
title: "ListSparrowDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSparrowDomains"
---

This interface is used to get a list of CDN domains to which the specified function can be bound.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListSparrowDomains&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListSparrowDomains<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the ID of the function for which you want to bind to domain.<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Domains<br><br>  |  <br><br>[]Domain<br><br>  |  <br><br>Domain List<br><br>  |  <br><br>See the explanation below.<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total number of functions<br><br>  |  <br><br>1<br><br>  |

### Domain

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Domain<br><br>  |  <br><br>String<br><br>  |  <br><br>Domain<br><br>  |  <br><br>test.sparrow1.com<br><br>  |
|  <br><br>BindStatus<br><br>  |  <br><br>Int32<br><br>  |  <br><br>The binding status between the domain name and the specified function:<br><br>  <br><br> <br> <br><br>* 1: Already bound<br><br><br> <br> <br><br>* 2: Can be bound<br><br><br> <br> <br><br>* 3: Cannot be bound<br><br><br>  <br><br>  |  <br><br>2<br><br>  |

## Samples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListSparrowDomains&Version=2021-03-01
&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****
&Page=1
&Limit=10
```

### Sample Response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2023050920020063355B94DB6C32617243",
    "Action": "ListSparrowDomains",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
        "Domains": [
            {
                "BindStatus": 2,
                "Domain": "test.sparrow1.com"
            }
        ],
        "TotalCount": 1
  }
}
```
