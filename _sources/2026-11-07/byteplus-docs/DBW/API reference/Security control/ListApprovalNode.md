---
title: "ListApprovalNode"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ListApprovalNode"
---

Call the ListApprovalNode API to query approval nodes.

<span id="ZKFDHIh1"></span>
## Request type

Synchronous request.

<span id="DmuvJv85"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |Page number. The value range is 1 to 1000, with a default of 1. |1 |
|PageSize |Integer |Yes |Number of records per page. The value range is 1 to 1000, with a default of 10. |10 |
|NodeId |String<br><br> |No<br><br> |Approval Node ID.<br><br> |0<br><br> |
|NodeName |String |No |Approval node name |DBA |


<span id="rXrLuTPE"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|[ApprovalNodes](https://docs.byteplus.com/en/docs/DBW/data-structure#MD0J8VyY) |Object[] |Approval node information. |See the response example. |
|Total |String |The number of nodes that meet the query criteria returned. |1 |


<span id="FHlKpu5A"></span>
## Request example

```JSON
POST /?Action=ListApprovalNode&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "PageNumber": 1,
    "PageSize": 10,
    "NodeId": "0",
    "NodeName": "DBA"
}
```


<span id="qFiY3IqL"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202509241537102F907E385B3409B6D565-93e601",
        "Action": "ListApprovalNode",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "ApprovalNodes": [
            {
                "ApprovalUsers": [
                    {
                        "UserId": "",
                        "UserName": ""
                    }
                ],
                "CreateUser": {
                    "UserId": "",
                    "UserName": ""
                },
                "Memo": "DBA",
                "NodeId": "0",
                "NodeName": "DBA",
                "NodeType": "System"
            }
        ],
        "Total": 1
    }
}
```


<span id="TM1tWcBG"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
