---
title: "ModifyParameterTemplate"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyParameterTemplate"
---

Call the ModifyParameterTemplate API to modify a parameter template.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyParameterTemplate&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|TemplateId |String |Yes |vedbmpt\-5j37992t\*\*\*\* |Parameter templates ID. |
|TemplateName |String |Yes |Template_test |Name of the parameter template. |
|TemplateParameters |Array of [OverrideParameterObject](https://docs.byteplus.com/en/docs/265/92460#overrideparameterobject) |Yes |See the request example. |The parameters and parameter values included in the parameter template. |
|TemplateDescription |String |No |Description information |Parameter template description, with a content length of 0 to 200 characters. |


<span id="overrideparameterobject"></span>
### OverrideParameterObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ParameterName |String |Yes |auto_increment_increment |Parameter name. |
|ParameterValue |String |No |1 |Parameter running value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |vedbmpt\-5j37992t\*\*\*\* |Parameter templates ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TemplateId": "vedbmpt-5j37992t****",
    "TemplateName": "Template_test",
    "TemplateParameters": [
        {
            "ParameterName": "auto_increment_increment",
            "ParameterValue": "1"
        }
    ],
    "TemplateDescription": "描述信息"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyParameterTemplate",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "TemplateId": "vedbmpt-5j37992t****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
