---
title: "DescribeParameterTemplates"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplates"
---

Call the DescribeParameterTemplates to query the parameter template list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeParameterTemplates&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|TemplateName |String |No |template_test |Name of the parameter template. |
|TemplateId |String |No |vedbmpt\-5j37992t\*\*\*\* |Parameter templates ID. |
|TemplateCategory |String |No |DBEngine |The classification for the parameter template, with a default value of `DBEngine`. |
|TemplateType |String |No |MySQL |Database type of the parameter template. The default value is `MySQL`. |
|TemplateTypeVersion |String |No |MySQL_8_0 |The database engine version for the parameter template. The valid values are:<br><br><br>* `MySQL_5_7`: MySQL version 5.7.<br><br>* `MySQL_8_0`: MySQL version 8.0. |
|TemplateSource |String |No |User |The type of the parameter templates. Values:<br><br><br>* `User`: User template.<br><br>* `System`: System template. |
|PageSize |Integer |Yes |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |
|PageNumber |Integer |Yes |1 |The page number, which must be greater than or equal to 1 and not exceed the maximum value of an Integer. The default is 1. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |The total number of returned results. |
|TemplateInfos |Array of [TemplateInfoObject](https://docs.byteplus.com/en/docs/265/57397#templateinfoobject) |Refer to the return example. |Parameter template details. |


<span id="templateinfoobject"></span>
### TemplateInfoObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |vedbmpt\-5j37992t\*\*\*\* |Parameter templates ID. |
|TemplateName |String |template_test |Name of the parameter template. |
|TemplateCategory |String |DBEngine |The classification for the parameter template, with a default value of `DBEngine`. |
|TemplateDescription |String |Description |Parameter template description, with a content length of 0 to 200 characters. |
|TemplateTypeVersion |String |MySQL_8_0 |The database engine version for the parameter template. The valid values are:<br><br><br>* `MySQL_5_7`: MySQL version 5.7.<br><br>* `MySQL_8_0`: MySQL version 8.0. |
|TemplateSource |String |User |The type of the parameter templates. Values:<br><br><br>* `System`: System template.<br><br>* `User`: User template. |
|ParameterNumber |Integer |6 |The number of parameters in the parameter template. |
|NeedRestart |Boolean |true |Whether the parameter template contains parameters that require an instance restart to take effect. |
|CreateTime |String |2022\-10\-10 10:10:37 |Parameter template creation time. |
|UpdateTime |String |2022\-10\-10 10:10:37 |Modification time of the parameter template. |
|TemplateType |String |MySQL |Database type of the parameter template. The default value is `MySQL`. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeParameterTemplates&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TemplateId": "vedbmpt-5j37992t****",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025022811260336F1105012D3D74618B5-3063f3",
        "Action": "DescribeParameterTemplates",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "TemplateInfos": [
            {
                "CreateTime": "2025-02-28T02:46:03Z",
                "NeedRestart": false,
                "ParameterNumber": 1,
                "TemplateCategory": "DBEngine",
                "TemplateDescription": "desc",
                "TemplateId": "vedbmpt-5j37992t****",
                "TemplateName": "template_test",
                "TemplateSource": "User",
                "TemplateType": "MySQL",
                "TemplateTypeVersion": "MySQL_8_0",
                "UpdateTime": "2025-02-28T02:46:03Z"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
