---
title: "ListContinent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListContinent"
---

This interface is used to get a list of continents where the cluster is located.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListContinent&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListContinent<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function id<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |

## Response Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Continents<br><br>  |  <br><br>[]Continent<br><br>  |  <br><br>The array of continents where the cluster is located.<br><br>  |  <br><br>["Asia"]<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListContinent&Version=2021-03-01
&FunctionId=3gyz993****
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListContinent",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Continents": [
            "Asia"
        ]
    }
}
```
