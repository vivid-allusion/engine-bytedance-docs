---
title: "DescribeTemplateOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateOperations_en-us"
---

Gets the operation history of a specified policy. The operation history can contain up to 10 records.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeTemplateOperations`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Represents the ID of the policy to query. |`tpl-s5wzdn0` |
|PageSize |Long |No |This API paginates the retrieved records. This parameter indicates the number of records per page. The value can range from 1 to 50, and the default value is `10`. |`10` |
|PageNum |Long |No |Indicates which page of records to display. The value of this parameter can only be `1`, which is also the default value. |`1` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Operations |Object[] |Represents the operation history of the specified policy, containing up to 10 records. The records in the list are sorted by `OperateTime`, with the first record corresponding to the most recent operation. | |
|Action |String |Represents the recorded operation. This parameter has the following values:<br><br><br>* `bind`: Indicates domain name binding.<br><br>* `create`: Indicates policy creation.<br><br>* `release`: Indicates policy publish. |`bind` |
|DomainsAfter |Object[] |If `Action` is `bind`, this parameter represents the bound domain name information. If `Action` is not `bind`, the parameter value is `null`. | |
|Domain |String |Represents the bound domain name. |`abc.example.com` |
|DomainsBefore |Object[] |If `Action` is `bind`, this parameter represents the domain name information bound to the policy before the binding operation.<br><br>In any of the following cases, the parameter value is `null`:<br><br><br>* `Action` is not `bind`.<br><br>* The recorded operation is the first time a domain name is bound. | |
|Domain |String |Represents the domain name bound to the policy before the binding operation. |`www.example.com` |
|OperateTime |Long |Represents the recorded operation time in Unix timestamp format, accurate to the second. |`1755314680` |
|Total |Long |Represents the number of records in the operation history. |`3` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021-03-01
{
    "TemplateId": "tpl-s5wzdn0"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910090657D2AD1B292BAAA8BF5384",
        "Action": "DescribeTemplateOperations",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Operations": [
            {
                "Action": "release",
                "DomainsAfter": [
                    {
                        "Domain": "www.example.com"
                    }
                ],
                "DomainsBefore": [
                    {
                        "Domain": "abc.example.com"
                    }
                ],
                "OperateTime": 1755323476
            },
            {
                "Action": "bind",
                "DomainsAfter": [
                    {
                        "Domain": "abc.example.com"
                    }
                ],
                "DomainsBefore": null,
                "OperateTime": 1755314680
            },
            {
                "Action": "release",
                "DomainsAfter": null,
                "DomainsBefore": null,
                "OperateTime": 1755312538
            },
            {
                "Action": "create",
                "DomainsAfter": null,
                "DomainsBefore": null,
                "OperateTime": 1755309241
            }
        ],
        "Total": 4
    }
}
```


&nbsp;
