---
title: "Error code overview"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Error-code-overview"
---

When you encounter an error while using DMS, it will return ErrorCode and ErrorDetail information to help you quickly identify and resolve the issue.

<span id="f296162d"></span>
## Error response example

```Bash
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "QueryDataMigrateTask",
        "Version": "2018-01-01",
        "Service": "dms",
        "Region": "ap-southeast-1",
        "ErrorInfo": {
            "ErrorCode": "1003-00000001",
            "ErrorDetail": "do list objects on source failed"
        }
    }
}
```


The explanation of the response parameters is as follows:


|**Response parameters** |**Description** |
|---|---|
|ErrorCode |DMS provides more granular error codes, each error corresponds to a unique ErrorCode, facilitating quick problem identification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only the QueryDataMigrateTask and ListDataMigrateTask interfaces return ErrorCode.</div><br> |
|ErrorDetail |Error detail description. |
