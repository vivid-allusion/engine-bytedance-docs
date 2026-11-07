---
title: "DescribeDBInstanceParametersLog"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparame"
---

Call the DescribeDBInstanceParametersLog API to query the modification history of an instance parameter.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|StartTime |String |Yes |2023\-03\-01T00:00:00.000Z |Query start time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|EndTime |String |Yes |2023\-03\-01T10:00:00.000Z |Query end time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PageNumber |Integer |No |1 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |10 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of records returned by the query. |
|ParameterChangeLogs |Array of [ParameterChangeLogObject](https://docs.byteplus.com/en/docs/61/15724#parameterchangelogobject) |Refer to the sample response. |Parameter modification history list. |


<span id="parameterchangelogobject"></span>
### ParameterChangeLogObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |innodb_stats_sample_pages |Parameter name. |
|Status |String |Applied |State. Values:<br><br><br>* `Applied`: effective.<br><br>* `Invalid`: not effective.<br><br>* `Syncing`: applying, not yet effective. |
|NewValue |String |3 |Parameter value (after applying template). |
|OldValue |String |8 |Parameter value (before applying template) |
|ModifyTime |String |2020\-03\-01T00:00:00.000Z |Timestamp for modifying parameters. Format: yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceParametersLog&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-4cdcae5e****",
    "StartTime": "2023-08-03T12:14:36.000Z",
    "EndTime": "2023-08-04T23:59:59.000Z"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230804120139EC3486A726561A0DDAE6",
        "Action": "DescribeDBInstanceParametersLog",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ParameterChangeLogs": [
            {
                "ModifyTime": "2023-08-03TZ12:22:41.000Z",
                "Name": "wal_level",
                "NewValue": "LOGICAL",
                "OldValue": "replica",
                "Status": "Applied"
            }
        ],
        "Total": 1
    }
}
```
