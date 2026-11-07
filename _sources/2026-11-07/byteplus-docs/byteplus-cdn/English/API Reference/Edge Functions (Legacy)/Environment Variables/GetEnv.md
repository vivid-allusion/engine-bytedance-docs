---
title: "GetEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetEnv"
---

This interface is used to retrieve the environment variables of a function based on the function id.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=GetEnv&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>GetEnv<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function id<br><br>  |  <br><br>23455331245<br><br>  |

## Response Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Envs<br><br>  |  <br><br>[]Env<br><br>  |  <br><br>List of function variables<br><br>  |  <br><br>See the explanation below<br><br>  |

**Env**

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Key<br><br>  |  <br><br>String<br><br>  |  <br><br>The key of the environment variable<br><br>  |  <br><br>a<br><br>  |
|  <br><br>Value<br><br>  |  <br><br>String<br><br>  |  <br><br>The value of the environment variable<br><br>  |  <br><br>a<br><br>  |

## Example

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetEnv&Version=2021-03-01
&FunctionId=23455331245
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "GetEnv",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Envs": [
            {
                "Key": "abc",
                "Value": "123"
            }
        ]
    }
}
```
