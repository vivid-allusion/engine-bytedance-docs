---
title: "DescribeWorkflow"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeWorkflow"
---

Call the DescribeWorkflow API to query the details of an approval work order.

<span id="LByVBO3g"></span>
## Request type

Synchronous request.

<span id="UqXPQtRF"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Description** |**Sample** |
|---|---|---|---|---|
|TicketId |String |Yes |Ticket number. |178887541272244\*\*\*\* |


<span id="8yKzSZm3"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|NodeName |String |Approval node name. |Owner |
|Operator |String |Current handler name.<br><br>If there are multiple current handlers, separate each with an English comma (,). |huahua,csy,testcsy,cyg,dbw_subuser,dbw_bot |
|OperatorId |String |Current handler ID.<br><br>If there are multiple current handlers, separate each with an English comma (,). |473270,497392,1543634,1251643,1261592,2100067216dbw_bot |
|Status |String |Approval status with the following return values.<br><br><br>* `Undo`: Not started<br><br>* `Approval`: In progress<br><br>* `Pass`: Approved<br><br>* `Reject`: Rejected<br><br>* `Cancel`: approval revoked |Undo |
|UpdateTime |String |Update time. |2025\-08\-21 14:56:21 |
|step |Long |Approval node sequence. |3 |


<span id="iNgfCsX1"></span>
## Request example

```JSON
POST /?Action=DescribeWorkflow&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "TicketId": "178887541272244****"
}
```


<span id="fTVtyMUN"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250821160910A289857ABABC59AC93C8-47e8a2",
        "Action": "DescribeWorkflow",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": "Success",
        "ErrMsg": "",
        "FlowNodes": [
            {
                "NodeName": "Owner",
                "Operator": "RootAccount",
                "OperatorId": "2100067216",
                "Status": "Pass",
                "UpdateTime": "2025-08-21 14:56:21",
                "step": 1
            },
            {
                "NodeName": "DBA",
                "Operator": "",
                "OperatorId": "",
                "Status": "Approval",
                "UpdateTime": "",
                "step": 2
            },
            {
                "NodeName": "Admin",
                "Operator": "huahua,csy,testcsy,cyg,dbw_subuser,dbw_bot",
                "OperatorId": "473270,497392,1543634,1251643,1261592,2100067216dbw_bot",
                "Status": "Undo",
                "UpdateTime": "",
                "step": 3
            }
        ]
    }
}
```


<span id="wurZZTFg"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
