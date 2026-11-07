---
title: "ManualExecuteTicket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ManualExecuteTicket"
---

Call the ManualExecuteTicket interface to manually execute the ticket.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This interface is only used for tickets with an execution type of <code>Manual</code> and a status of <code>TicketWaitExecute</code>. The ticket status can be queried via the DescribeTicketDetail interface.</div>


<span id="5t4qSUGz"></span>
## Request type

Synchronous request.

<span id="2nJ5Lh7d"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Description** |**Sample** |
|---|---|---|---|---|
|TicketId |String |Yes |Ticket number. |178887541272244\*\*\*\* |


<span id="h7nCtUyB"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|Code |String |Execution result, with the following return values.<br><br><br>* `success`: Success<br><br>* `false`: Failure |success |
|ErrMsg |String<br><br> |Error message.<br><br>When the return value of `code` is `success`, the return value of `ErrMsg` is empty. |\- |


<span id="ptJRmtFf"></span>
## Request example

```JSON
POST /?Action=ManualExecuteTicket&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "TicketId": "178887541272244****"
}
```


<span id="ndHD2Pdn"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025081116271262AB5D7804D0BA0424CF-d56ae5",
        "Action": "ManualExecuteTicket",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": "success",
        "ErrMsg": ""
    }
}
```


<span id="hKMoY5H2"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
