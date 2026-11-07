---
title: "SetIncrementalSyncInterval - Set automatic incremental synchronization interval"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/SetIncrementalSyncInterval"
---

Call the SetIncrementalSyncInterval operation to specify the interval for automatic incremental synchronization.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=SetIncrementalSyncInterval&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|tIYGtY">必选</span> `Sample value: SetIncrementalSyncInterval`

The operation that you want to perform. Valid value: SetIncrementalSyncInterval.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|9jFY1w">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**MigrationJobId ** <span data-label="purple">string </span><span data-api-tag="require|T9VPCW">必选</span> `Sample value: job-3tiegs1y963vj0******`

The migration task ID. You can call the [DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) operation to query and obtain the migration task ID.



**SyncInterval ** <span data-label="purple">integer </span>`Optional` `Sample value: 2`

The incremental synchronization interval. Unit: hours.


* Valid range: 0\-168

* Maximum value: 168

* Minimum value: 1



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=SetIncrementalSyncInterval&Version=2020-04-01&MigrationJobId=job-3tiegs1y963vj0****&SyncInterval=2 HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202306051643546E59A4A3E62D****",
    "Action": "SetIncrementalSyncInterval",
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
|400 |InvalidJobConfigForIncrementalSync.Unsupported |The specified migration job does not support incremental sync. |The specified migration task does not support incremental migration. |
|400 |InvalidJobStateForUpdateSyncInterval.Unsupported |The specified migration job state does not support update sync interval. |The incremental synchronization frequency cannot be modified for the migration task. |
|400 |LimitExceeded.MaximumSyncInterval |The number of specified SyncInterval exceeds the maximum limit. |The specified SyncInterval value exceeds the upper limit. |
|400 |LimitExceeded.MinimumSyncInterval |The number of specified SyncInterval exceeds the minimum limit. |The specified SyncInterval value is below the lower limit. |
|400 |MissingParameter.MigrationJobId |The required parameter MigrationJobId is not supplied. |The MigrationJobId parameter cannot be empty. |
|404 |InvalidMigrationJob.NotFound |The specified migration job does not exist. |The specified migration task does not exist. |
