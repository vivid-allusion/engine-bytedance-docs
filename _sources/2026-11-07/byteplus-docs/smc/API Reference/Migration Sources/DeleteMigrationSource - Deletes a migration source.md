---
title: "DeleteMigrationSource - Deletes a migration source"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/DeleteMigrationSource"
---

Call the DeleteMigrationSource operation to delete a migration source.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteMigrationSource&groupName=%E8%BF%81%E7%A7%BB%E6%BA%90&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|T1gtX2">必选</span> `Sample value: DeleteMigrationSource`

The operation that you want to perform. Valid value: DeleteMigrationSource.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|3PaTLW">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**SourceId ** <span data-label="purple">string </span><span data-api-tag="require|1zOBxj">必选</span> `Sample value: s-3tiegs1y963vj0******`

The migration source ID. You can call the [DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) operation to query and obtain the migration source ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteMigrationSource&Version=2020-04-01&SourceId=s-3tiegs1y963vj0**** HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteMigrationSource",
        "Version": "2020-04-01",
        "Service": "smc",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidSourceStateForDelete.Unsupported |The specified migration source state does not support delete. |The migration source state does not support deletion. |
|400 |MissingParameter.SourceId |The required parameter SourceId is not supplied. |The SourceId parameter cannot be empty. |
|400 |InvalidJobStateForDelete.Unsupported |The specified migration job state does not support delete. |The current state of the specified migration task does not allow deletion. |
|404 |InvalidMigrationSource.NotFound |The specified migration source does not exist. |The specified migration source does not exist. |
|412 |InvalidMigrationSource.InUse |The specified migration source is in use. |A migration task is currently in progress for the specified migration source. |
