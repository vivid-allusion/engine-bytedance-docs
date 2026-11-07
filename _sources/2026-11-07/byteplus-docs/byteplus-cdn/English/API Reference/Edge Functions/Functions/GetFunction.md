---
title: "GetFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetFunction-en"
---

Gets detailed information about a specified function.

<span id="limits"></span>
## Limits

Request rate limit: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetFunction&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `GetFunction`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01` |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|AccountIdentity |Long |BytePlus account ID. |`20****` |
|UserIdentity |Long |This parameter is not used. Please ignore this parameter. | |
|ClazzName |String |This parameter is not used. Please ignore this parameter. | |
|BindingType |Integer |This parameter is not used. Please ignore this parameter. | |
|Domain |String[] |Domain name bound to the function. |`["example.com"]` |
|Name |String |Name of the function. |`hello-ve` |
|FunctionId |String |ID of the function. |`3gyz993****` |
|Status |Integer |Function status.<br><br><br>* 100: Running<br><br>* 400: Not associated<br><br>* 500: Configuring |`100` |
|IsPublish |Boolean |This parameter is not used. Please ignore this parameter. | |
|IsFullPublish |Boolean |This parameter is not used. Please ignore this parameter. | |
|CodeType |String |This parameter is not used. Please ignore this parameter. | |
|Creator |String |Username of the function creator. |`example` |
|CreateTime |Long |Creation time. Format is Unix timestamp (seconds). |`1638326159` |
|UpdateTime |Long |Update time. Format is Unix timestamp (seconds). |`1638326159` |
|Remark |String |Remarks for the function. |`this is a test` |
|ProjectName |String |Name of the project to which the function belongs. |`default` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetFunction&Version=2021-03-01&FunctionId=bc36dc7c58e942f0b9f125d186df****
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202404220913431B87E7D87928AD8F48BE",
        "Action": "GetFunction",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Function": {
            "AccountIdentity": 300000****,
            "UserIdentity": 0,
            "Domain": [
                "test.example.com"
            ],
            "Name": "test",
            "ClazzName": "Free",
            "BindingType": 0,
            "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
            "Status": 400,
            "IsPublish": false,
            "IsFullPublish": false,
            "CodeType": "js",
            "Creator": "test_user",
            "CreateTime": 1713776330,
            "UpdateTime": 1713776330,
            "Remark": "",
            "ProjectName": "default"
        }
    }
}
```
