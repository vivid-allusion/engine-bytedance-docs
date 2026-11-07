---
title: "DescribeDBInstanceEngineMinorVersions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceengineminorversions"
---

Call the DescribeDBInstanceEngineMinorVersions API to query the upgradable minor kernel versions of an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |No |["mysql\-19f81673\*\*\*\*"] |The instance ID(s) for which to query the upgradable kernel versions. Supports batch querying by passing multiple IDs.<br><br>tip<br><br><br>* If no instance ID is provided, returns the minor kernel versions for all active instances under the account.<br><br>* If a single instance ID is provided, returns the upgradable minor kernel versions for that instance.<br><br>* If multiple instance IDs are provided, these instances should have the same database version. In this case, the latest minor kernel version under that database version will be returned. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|KernelVersions |String[] |[<br><br>"MySQL 5.7.32_20240315",<br><br>"MySQL 5.7.32_20240216",<br><br>"MySQL 5.7.32_20240416",<br><br>"MySQL 5.7.32_20240415",<br><br>"MySQL 8.0.32_20241015",<br><br>"MySQL 5.7.32_20241018",<br><br>"MySQL 5.7.32_20240618",<br><br>"MySQL 5.7.32_20240615",<br><br>"MySQL 8.0.32_20240816",<br><br>"MySQL 8.0.32_20241021",<br><br>"MySQL 5.7.32_20241015",<br><br>"MySQL 5.7.32_20241021",<br><br>"MySQL 5.7.32_20241020",<br><br>"MySQL 8.0.26_20240316"<br><br>] |The upgradable minor kernel versions of the instance. |

## Sample request 1

Query the upgradable minor kernel versions of a single instance.

```json
POST /?Action=DescribeDBInstanceEngineMinorVersions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-19f81673add7"
    ]
}
```

## Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202412192015432E3286F81118CC551BB1-296bdf",
        "Action": "DescribeDBInstanceEngineMinorVersions",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "KernelVersions": [
            "MySQL 8.0.32_20241216",
            "MySQL 8.0.32_20241215",
            "MySQL 8.0.32_20241021",
            "MySQL 8.0.32_20241020",
            "MySQL 8.0.32_20241019",
            "MySQL 8.0.32_20241018",
            "MySQL 8.0.32_20241017",
            "MySQL 8.0.32_20241016"
        ]
    }
}
```

## Sample request 2

Query the upgradable minor kernel versions for multiple instances.

```json
POST /?Action=DescribeDBInstanceEngineMinorVersions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-19f81673****",
        "mysql-67bda593****"
    ]
}
```

## Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202412192013409B15FAFEFF272039AC91-0552e5",
        "Action": "DescribeDBInstanceEngineMinorVersions",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "KernelVersions": [
            "MySQL 8.0.32_20241216"
        ]
    }
}
```

## Sample request 3

Query all available minor kernel versions that can be upgraded for in\-use instances under the current account."

```json
POST /?Action=DescribeDBInstanceEngineMinorVersions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```

## Sample response 3

```json
{
    "ResponseMetadata": {
        "RequestId": "202412192016072E3286F81118CC55263E-166a2c",
        "Action": "DescribeDBInstanceEngineMinorVersions",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "KernelVersions": [
            "MySQL 5.7.32_20240315",
            "MySQL 5.7.32_20240216",
            "MySQL 5.7.32_20240416",
            "MySQL 5.7.32_20240415",
            "MySQL 8.0.32_20241015",
            "MySQL 5.7.32_20241018",
            "MySQL 5.7.32_20240618",
            "MySQL 5.7.32_20240615",
            "MySQL 8.0.32_20240816",
            "MySQL 8.0.32_20241021",
            "MySQL 5.7.32_20241015",
            "MySQL 5.7.32_20241021",
            "MySQL 5.7.32_20241020",
            "MySQL 8.0.26_20240316",
            "MySQL 5.7.32_20241216",
            "MySQL 8.0.32_20241216"
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
