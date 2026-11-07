---
title: "DeleteMigrationJob - Deletes a migration task"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/DeleteMigrationJob"
---

Call the DeleteMigrationJob operation to delete a migration task.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteMigrationJob&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zOclop">必选</span> `Sample value: DeleteMigrationJob`

The operation that you want to perform. Valid value: DeleteMigrationJob.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|tt4urI">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**MigrationJobId ** <span data-label="purple">string </span><span data-api-tag="require|sAQ4t9">必选</span> `Sample value: job-3tiegs1y963vj0******`

The migration task ID. You can call the [DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) operation to query and obtain the migration task ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteMigrationJob&Version=2020-04-01&MigrationJobId=job-3tiegs1y963vj0**** HTTP/1.1
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
        "Action": "DeleteMigrationJob",
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
|400 |InvalidJobStateForDelete.Unsupported |The specified migration job state does not support delete. |The current state of the specified migration task does not allow deletion. |
|400 |MissingParameter.MigrationJobId |The required parameter MigrationJobId is not supplied. |The MigrationJobId parameter cannot be empty. |
|404 |InvalidMigrationJob.NotFound |The specified migration job does not exist. |The specified migration task does not exist. |
