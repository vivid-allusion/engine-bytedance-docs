---
title: "DeleteEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteEnv"
---

This interface is used to delete the environment variables of a function based on the function id.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: https://cdn.byteplusapi.com/?Action=DeleteEnv&Version=2021\-03\-01

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>DeleteEnv<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function id<br><br>  |  <br><br>23455331245<br><br>  |
|  <br><br>EnvKeys<br><br>  |  <br><br>[]EnvKeys<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The key of the environment variable you want to delete. You can delete multiple environment variables in one batch.<br><br>  |  <br><br>["abc","def"]<br><br>  |

## Response Parameters

None

## Example

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=DeleteEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        "abc",
        "def"
    ]
}
```
