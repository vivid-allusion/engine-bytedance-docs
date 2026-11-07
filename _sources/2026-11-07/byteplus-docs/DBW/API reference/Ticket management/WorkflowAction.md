---
title: "WorkflowAction"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/WorkflowAction"
---

Call the WorkflowAction API to approve a ticket.

<span id="X2yumWpU"></span>
## Request type

Synchronous request

<span id="Ulf4hwWH"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|TicketId |String |Yes |Ticket ID. |178887541272244\*\*\*\* |
|ActionType |String |No |Approval result, with the following values.<br><br><br>* `Pass`: (Default value) Approved.<br><br>* `Reject`: Reject. |Pass |


<span id="nT549uB1"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|Code |String |Ticket approval result, with the following values.<br><br><br>* `success`: Succeeded.<br><br>* `false`: Failed. |success |
|ErrMsg |String |Error message.<br><br>When `code` returns `success`, `ErrMsg` returns empty. |\- |


<span id="mm6TLRxv"></span>
## Request example

```JSON
POST /?Action=WorkflowAction&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
  "TicketId": "178887541272244****",
  "ActionType": "Pass"
}
```


<span id="VIgCU2ao"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202405101815074D6C61C22FD7E479870C-e62012",
        "Action": "WorkflowAction",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": "success",
        "ErrMsg":""
    }
}
```


<span id="bicq4moL"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
