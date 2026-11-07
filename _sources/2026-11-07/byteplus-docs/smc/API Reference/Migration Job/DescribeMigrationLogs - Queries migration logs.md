---
title: "DescribeMigrationLogs - Queries migration logs"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/DescribeMigrationLogs"
---

Call the DescribeMigrationLogs operation to query migration logs.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeMigrationLogs&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|hiYRGi">必选</span> `Sample value: DescribeMigrationLogs`

The operation that you want to perform. Valid value: DescribeMigrationLogs.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|mAlWJF">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**MigrationJobId ** <span data-label="purple">string </span><span data-api-tag="require|Jj3YTo">必选</span> `Sample value: job-3tiegs1y963vj0******`

The migration task ID. You can call the [DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) operation to query and obtain the migration task ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2023-05-01T12:00:00+08:00`

The time when the migration task is created.



**FinishedAt ** <span data-label="purple">string </span>`Sample value: 2023-05-01T14:00:00+08:00`

The time when the migration task finishes.



**Logs ** <span data-label="purple">object[] </span>`Sample value: --`

The information of the migration task log that meets the conditions.


**LogLevel ** <span data-label="purple">string </span>`Sample value: Info`

The log level. Valid values:


* Info: Information.

* Error: Error.



**LogMessage ** <span data-label="purple">string </span>`Sample value: Import KeyPair {kp-ycg7gbou35iju****} SUCCESS`

The log content.



**LogTime ** <span data-label="purple">string </span>`Sample value: 2023-05-01T12:00:00+08:00`

The log time.




**StartedAt ** <span data-label="purple">string </span>`Sample value: 2023-05-01T13:00:00+08:00`

The time when the migration task starts.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeMigrationJobs&Version=2020-04-01&MigrationJobId=job-3tiegs1y963vj0**** HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2023060516304100187394DCBD****",
        "Action":"DescribeMigrationLogs",
        "Version":"2020-04-01",
        "Service":"smc",
        "Region":"cn-beijing"
    },
    "Result":{
        "CreatedAt":"2023-05-31T15:44:07+08:00",
        "StartedAt":"2023-05-31T15:44:07+08:00",
        "FinishedAt":"2023-05-31T15:56:03+08:00",
        "Logs":[
            {
                "LogTime":"2023-05-31T15:44:07+08:00",
                "LogLevel":"Info",
                "LogMessage":"Start Migration job SUCCESS"
            },
            {
                "LogTime":"2023-05-31T15:56:03+08:00",
                "LogLevel":"Info",
                "LogMessage":"Finish Migration job SUCCESS"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MigrationJobId |The required parameter MigrationJobId is not supplied. |The MigrationJobId parameter cannot be empty. |
|404 |InvalidMigrationJob.NotFound |The specified migration job does not exist. |The specified migration task does not exist. |
|404 |InvalidMigrationJobLog.NotFound |The specified migration job log does not exist. |The specified migration task log does not exist. |
