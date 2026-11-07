---
title: "EditEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-EditEnv"
---

This interface is used to update the environment variables of a function based on the function id.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=EditEnv&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>EditEnv<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function id<br><br>  |  <br><br>23455331245<br><br>  |
|  <br><br>Envs<br><br>  |  <br><br>[]Env<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The configuration content<br><br>  |  <br><br>[{"Key": "abc","Value": "123"}]<br><br>  |

**Env**

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Key<br><br>  |  <br><br>String<br><br>  |  <br><br>The key of the environment variable<br><br>  |  <br><br>a<br><br>  |
|  <br><br>Value<br><br>  |  <br><br>String<br><br>  |  <br><br>The value of the environment variable<br><br>  |  <br><br>a<br><br>  |

## Response Parameters

None

## Example

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=EditEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        {
            "Key": "abc",
            "Value": "123"
        }
    ]
}
```
