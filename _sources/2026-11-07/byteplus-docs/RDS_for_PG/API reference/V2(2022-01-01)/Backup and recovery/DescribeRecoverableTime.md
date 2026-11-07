---
title: "DescribeRecoverableTime"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describerecoverabletime"
---

Call the DescribeRecoverableTime API to query the time range for data recovery from an instance backup.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RecoverableTimeInfo |Array of [RecoverableTimeInfoObject](https://docs.byteplus.com/en/docs/61/15714#recoverabletimeinfoobject) |2023\-10\-08T18:17:12.000Z |The earliest and latest restoration time of the instance (UTC time). Empty means the instance is currently not recoverable. |


<span id="recoverabletimeinfoobject"></span>
### RecoverableTimeInfoObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|EarliestRecoverableTime |String |2022\-01\-01T10:10:10.000Z |The earliest instance restoration time (UTC). Empty means the instance is currently not recoverable. |
|LatestRecoverableTime |String |2022\-01\-01T10:10:10.000Z |The latest instance restoration time (UTC). Empty means the instance is currently not recoverable. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeRecoverableTime&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080411193413E74BF9DC0908069420",
        "Action": "DescribeRecoverableTime",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RecoverableTimeInfo": [
            {
                "EarliestRecoverableTime": "2023-10-08T18:17:12.000Z",
                "LatestRecoverableTime": "2023-10-18T13:38:23.289Z"
            }
        ]
    }
}
```
