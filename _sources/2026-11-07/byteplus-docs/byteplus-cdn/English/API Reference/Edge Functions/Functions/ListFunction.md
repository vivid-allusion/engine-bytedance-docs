---
title: "ListFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en"
---

Gets the function list.

<span id="limits"></span>
## Limits

Request rate limit: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListFunction&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListFunction`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01` |
|Page |Integer |No |Page number. |
|Limit |Integer |No |Number of records per page. The default value is 100. The maximum is 100. |
|OrderBy |Integer |No |This parameter specifies the order of data query. It accepts the following values:<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |
|OrderType |String |No |Available sorting types are:<br><br><br>* create_time (default): Sort data by creation time.<br><br>* update_time: Sort data by last update time. |
|Status |String |No |Function status.<br><br><br>* 100: Running<br><br>* 400: Not associated<br><br>* 500: Configuring |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example Value |
|---|---|---|---|
|Functions |Object[] |Function list. | |
|AccountIdentity |Long |BytePlus account ID. |`20****` |
|UserIdentity |Long |This parameter is not used. Please ignore this parameter. |`0****` |
|Domain |String[] |Domain name associated with the function. |`["example.com"]` |
|Name |String |Name of the function. |`hello-ve` |
|ClazzName |String |This parameter is not used. Please ignore this parameter. | |
|BindingType |Integer |This parameter is not used. Please ignore this parameter. | |
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
|TotalCount |Long |Total number of functions |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunction&Version=2021-03-01
```


<span id="response-example"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202404220913221B87E7D87928AD8F42F8",
    "Action": "ListFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
        "Functions": [
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test1.example.com"
                ],
                "Name": "test1",
                "ClazzName": "Free",
                "BindingType": 200,
                "FunctionId": "54ac587666c148a6b9ffacbb0cb1****",
                "Status": 100,
                "IsPublish": true,
                "IsFullPublish": true,
                "CodeType": "js",
                "Creator": "example_user",
                "CreateTime": 1711004239,
                "UpdateTime": 1713270175,
                "Remark": "",
                "ProjectName": "default"
            },
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test2.example.com"
                ],
                "Name": "test",
                "ClazzName": "Free",
                "BindingType": 0,
                "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
                "Status": 400,
                "IsPublish": false,
                "IsFullPublish": false,
                "CodeType": "js",
                "Creator": "example_user",
                "CreateTime": 1713776330,
                "UpdateTime": 1713776330,
                "Remark": "",
                "ProjectName": "default"
            }
        ],
        "TotalCount": 2
    }
}
```
