---
title: "DescribeParameterTemplateDetail"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplateDetail"
---

Call DescribeParameterTemplateDetail to query parameter template details.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeParameterTemplateDetail&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|TemplateId |String |Yes |vedbmpt\-5j37992t\*\*\*\* |Parameter templates ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplates">DescribeParameterTemplates</a> API to query the parameter templates ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |vedbmpt\-5j37992t\*\*\*\* |Parameter templates ID. |
|TemplateName |String |template_test |Name of the parameter template. |
|TemplateCategory |String |DBEngine |The classification for the parameter template, with a default value of `DBEngine`. |
|TemplateDescription |String |test |Parameter template description, with a content length of 0 to 200 characters. |
|TemplateTypeVersion |String |MySQL_8_0 |The database engine version for the parameter template. The valid values are:<br><br><br>* `MySQL_5_7`: MySQL version 5.7.<br><br>* `MySQL_8_0`: MySQL version 8.0. |
|TemplateSource |String |User |The type of the parameter templates. Values:<br><br><br>* `System`: System template.<br><br>* `User`: User template. |
|ParameterNumber |Integer |6 |The number of parameters in the parameter template. |
|NeedRestart |Boolean |true |Whether the parameter template contains parameters that require a restart to take effect. |
|CreateTime |String |2022\-10\-10 10:10:37 |Parameter templates creation time. |
|UpdateTime |String |2022\-10\-10 10:10:37 |Modification time of the parameter template. |
|TemplateParameters |Array of [OverrideParameterObject](https://docs.byteplus.com/en/docs/265/57398#overrideparameterobject) |Refer to the return example. |The parameters and parameter values included in the parameter template. |
|TemplateType |String |MySQL |Database type of the parameter template. The default value is `MySQL`. |


<span id="overrideparameterobject"></span>
### OverrideParameterObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterName |String |auto_increment_increment |Parameter name. |
|ParameterValue |String |1 |Parameter running value. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeParameterTemplateDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TemplateId": "vedbmpt-5j37992t****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202502281127504EF4D8F43DBE31C83AE2-9d1be6",
        "Action": "DescribeParameterTemplateDetail",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreateTime": "2025-02-28T02:46:03Z",
        "NeedRestart": false,
        "ParameterNumber": 1,
        "TemplateCategory": "DBEngine",
        "TemplateDescription": "desc",
        "TemplateId": "vedbmpt-5j37992t****",
        "TemplateName": "template_test",
        "TemplateParameters": [
            {
                "ParameterName": "auto_increment_increment",
                "ParameterValue": "3"
            }
        ],
        "TemplateSource": "User",
        "TemplateType": "MySQL",
        "TemplateTypeVersion": "MySQL_8_0",
        "UpdateTime": "2025-02-28T02:46:03Z"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
