---
title: "CompareParameterTemplates"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CompareParameterTemplates"
---

Call the CompareParameterTemplates API to compare parameter templates.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CompareParameterTemplates&serviceCode=vedbm&version=2022-01-01&groupName=)

## Request parameters

|**Name** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|TemplateIds |Array of String |Yes |["vedbmpt\-u0eyakuv\*\*\*\*","vedbmpt\-3do8uhql\*\*\*\*"] |The parameter template ID. Only 2 parameter template IDs can be passed in.<br><br>> Description<br><br><br><br>* > Only parameter templates of the same type can be compared. System parameter templates cannot be compared with custom parameter templates.<br><br><br>* > Only parameter templates that apply to the same version can be compared.<br> |

## Response parameter

|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterComparisons |Array of [ParameterComparisonObject](https://docs.byteplus.com/en/docs/265/120430#parametercomparisonobject) |Refer to the Sample response. |Parameter template comparison details. |

### ParameterComparisonObject

|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterName |String |character_set_server |Parameter name. |
|TemplateParameters |Array of [TemplateParameterObject](https://docs.byteplus.com/en/docs/265/120430#templateparameterobject) |Refer to the Sample response. |Compare the parameter values in the parameter templates. |

### TemplateParameterObject

|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |vedbmpt\-u0eyakuv\*\*\*\* |Parameter templates ID. |
|ParameterValue |String |utf8mb4 |Parameter value. Returns `NOT_EXIST` if the parameter does not exist in another parameter template. |

## Example

### Request example

```JSON
POST /?Action=CompareParameterTemplates&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TemplateIds": [
        "vedbmpt-u0eyakuv****",
        "vedbmpt-3do8uhql****"
    ]
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202608271642450098A5D10DC41DADD46B-134c01",
        "Action": "CompareParameterTemplates",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "ParameterComparisons": [
            {
                "ParameterName": "character_set_server",
                "TemplateParameters": [
                    {
                        "ParameterValue": "utf8mb4",
                        "TemplateId": "vedbmpt-u0eyakuv****"
                    },
                    {
                        "ParameterValue": "utf8mb4",
                        "TemplateId": "vedbmpt-3do8uhql****"
                    }
                ]
            },
            {
                "ParameterName": "collation_server",
                "TemplateParameters": [
                    {
                        "ParameterValue": "utf8mb4_general_ci",
                        "TemplateId": "vedbmpt-u0eyakuv****"
                    },
                    {
                        "ParameterValue": "utf8mb4_0900_ai_ci",
                        "TemplateId": "vedbmpt-3do8uhql****"
                    }
                ]
            },
            {
                "ParameterName": "tmp_table_size",
                "TemplateParameters": [
                    {
                        "ParameterValue": "NOT_EXIST",
                        "TemplateId": "vedbmpt-u0eyakuv****"
                    },
                    {
                        "ParameterValue": "18446744073709551615",
                        "TemplateId": "vedbmpt-3do8uhql****"
                    }
                ]
            }
        ]
    }
}
```

## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
