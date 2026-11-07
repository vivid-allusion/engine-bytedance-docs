---
title: "ListFunctionDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-en"
---

Gets a list of domains that can be associated with a specified function.

<span id="limits"></span>
## Limits

Request rate limit: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListFunctionDomains`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01` |
|FunctionId |String |Yes |Enter the ID of the function you want to associate with the domain. |
|Page |Integer |Yes |Page number. |
|Limit |Integer |Yes |Number of items per page. The maximum is 50. |
|OrderBy |Integer |No |This parameter specifies the order of data. You can specify the following values:<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|Domains |Object[] |Domain list. |`["test.example.com"]` |
|Domain |String |Domain |`test.example.com` |
|BindStatus |Integer |Binding status between the domain and the specified function:<br><br><br>* 1: Bound<br><br>* 2: Can be bound<br><br>* 3: Cannot be bound |`2` |
|TotalCount |Integer |Total number of domains. |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****&Page=1&Limit=10
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2023050920020063355B94DB6C32617243",
        "Action": "ListFunctionDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "Domain": "123.example.com",
                "BindStatus": 2
            },
            {
                "Domain": "test.example.com",
                "BindStatus": 2
            }
        ],
        "TotalCount": 3
    }
}
```
