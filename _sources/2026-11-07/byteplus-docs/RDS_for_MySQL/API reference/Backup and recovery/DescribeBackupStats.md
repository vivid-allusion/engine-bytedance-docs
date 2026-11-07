---
title: "DescribeBackupStats"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackupstats"
---

Call the DescribeBackupStats API to query the storage space usage information of backup files for an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-cf4f3ddc\*\*\*\* |Instance ID. |
|ProjectName |String |No |default |The project to which the instance belongs. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mysql\-cf4f3ddc\*\*\*\* |Instance ID. |
|ProjectName |String |default |The project to which the instance belongs. |
|UsageStats |Object[] |Please refer to the response example. |Statistics of backup storage space usage. |
|Quantity |Long |254751807 |Statistics of usage. Unit: Byte. |
|StatItem |String |TotalBasicSpaceUsage |Statistics items.<br><br><br>* TotalBasicSpaceUsage: The storage space usage of the basic backup.<br><br>* BasicDataBackupUsage: The storage space usage of the local data backup.<br><br>* BasicBinlogBackupUsage: The storage space usage of the local log backup.<br><br>* TotalCrossRegionSpaceUsage: The storage space usage of the cross\-region backup.<br><br>* CrossRegionDataBackupUsage: The storage space usage of the cross\-region data backup.<br><br>* CrossRegionBinlogBackupUsage: The storage space usage of the cross\-region log backup. |
|StatTime |String |2024\-10\-15T08:13:45.000Z |Counting time. |

## Sample request

```json
POST /?Action=DescribeBackupStats&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-cf4f3ddc****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241015162054281DA795450D07933B34-5c0ce6",
        "Action": "DescribeBackupStats",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "InstanceId": "mysql-cf4f3ddc****",
        "ProjectName": "",
        "UsageStats": [
            {
                "Quantity": 254751807,
                "StatItem": "TotalBasicSpaceUsage",
                "StatTime": "2024-10-15T08:13:45.000Z"
            },
            {
                "Quantity": 132250077,
                "StatItem": "TotalCrossRegionSpaceUsage",
                "StatTime": "2024-10-15T08:13:45.000Z"
            },
            {
                "Quantity": 96760802,
                "StatItem": "BasicDataBackupUsage",
                "StatTime": "2024-10-15T08:13:45.000Z"
            },
            {
                "Quantity": 76523833,
                "StatItem": "CrossRegionDataBackupUsage",
                "StatTime": "2024-10-15T08:13:45.000Z"
            },
            {
                "Quantity": 157991005,
                "StatItem": "BasicBinlogBackupUsage",
                "StatTime": "2024-10-15T08:13:45.000Z"
            },
            {
                "Quantity": 55726244,
                "StatItem": "CrossRegionBinlogBackupUsage",
                "StatTime": "2024-10-15T08:13:45.000Z"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
