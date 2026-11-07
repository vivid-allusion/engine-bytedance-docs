---
title: "DescribeTemplateDomainOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomainOperations_en-us"
---

Gets the operation history of a specified domain name. The operation history can contain up to 10 records.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeTemplateDomainOperations`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Represents the domain name to query. |`www.example.com` |
|PageSize |Long |No |This API paginates the retrieved records. This parameter indicates the number of records per page. The value can range from 1 to 50, and the default value is `10`. |`10` |
|PageNum |Long |No |Indicates which page of records to display. The value of this parameter can only be `1`, which is also the default value. |`1` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Operations |Object[] |Represents the operation history of the specified domain name, containing up to 10 records. The records in the list are sorted by `OperateTime`, with the first record corresponding to the most recent operation. | |
|Action |String |Represents the recorded operation. This parameter has the following values:<br><br><br>* `create`: Indicates domain name creation.<br><br>* `update`: Indicates configuration update. |`create` |
|ConfigAfter |String |Represents the updated domain name configuration, including the following information:<br><br><br>* Bound delivery policy ID.<br><br>* Bound encryption policy ID.<br><br>* Bound rules engine policy ID.<br><br>* Whether HTTPS encryption service is enabled.<br><br>* Associated certificate ID.<br><br>* Service area.<br><br>* Whether WAF is enabled.<br><br><br>This parameter is a JSON string containing serialized domain name configuration information. | |
|ConfigBefore |String |If `Action` is `update`, this parameter represents the domain name configuration before the update. If `Action` is `create`, the parameter value is `null`. | |
|OperateTime |Long |Represents the recorded operation time in Unix timestamp format, accurate to the second. |`1755314680` |
|Total |Long |Represents the number of records in the operation history. |`3` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910092134B929D683A64BF500C428",
        "Action": "DescribeTemplateDomainOperations",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Operations": [
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747921048
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747921044
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747900254
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747900155
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747899947
            },
            {
                "Action": "create",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "",
                "OperateTime": 1747795591
            }
        ],
        "Total": 6
    }
}
```


&nbsp;
