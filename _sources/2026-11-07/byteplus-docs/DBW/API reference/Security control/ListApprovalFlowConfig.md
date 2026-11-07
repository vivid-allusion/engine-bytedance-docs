---
title: "ListApprovalFlowConfig"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ListApprovalFlowConfig"
---

Call the ListApprovalFlowConfig API to query the approval workflow list.

<span id="khefaLBS"></span>
## Request type

Synchronize request.

<span id="AEZQ7GdP"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |Page number. The value range is 1 to 1000, with a default of 1. |1 |
|PageSize |Integer |Yes |Number of records per page. The value range is 1 to 1000, with a default of 10. |10 |
|ConfigId |String<br><br> |No<br><br> |Approval workflow ID. |1822910882196242432 |
|ConfigName |String |No |Approval workflow name. |Single Approval Workflow |


<span id="r2SN7vbi"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|[FlowConfigs](https://docs.byteplus.com/en/docs/DBW/data-structure#So9Z8mJz) |Object[] |Returns the approval workflow information. |See the response example. |
|Total |String |The number of returned approval workflows. |1 |


<span id="RELaGUOF"></span>
## Request example

```JSON
POST /?Action=ListApprovalFlowConfig&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "PageNumber": 1,
    "PageSize": 10,
    "ConfigId": "1811243361378508800",
    "ConfigName": "cx-test-only"
}
```


<span id="sRFIbf61"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025092415382615E2F9128B24EAD318D8-563745",
        "Action": "ListApprovalFlowConfig",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "FlowConfigs": [
            {
                "AssociatedInstanceNum": 1,
                "ConfigId": "1811243361378508800",
                "ConfigName": "cx-test-only",
                "CreateUser": {
                    "UserId": "2100067216",
                    "UserName": "RootAccount"
                },
                "Memo": "管理员单点",
                "Type": "Customize"
            }
        ],
        "Total": 1
    }
}
```


<span id="jXe6ZIE3"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
