---
title: "DescribeDBInstanceSpecs"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs"
---

Call the DescribeDBInstanceSpecs API to query instance specifications available for sale.

## Request type

Synchronous request.

## Precautions

None of the request parameters for this API has a default value. When a parameter is not specified, the query does not filter by that parameter and proceeds based on other specified query conditions.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|ZoneId |String |No |cn\-beijing\-a |Primary availability zone ID. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) API to query the list of availability zones. |
|DBEngineVersion |String |No |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|SpecCode |String |No |rds.postgres.1c2g |instance specification code.<br><br>> **tip**<br><br><br>> For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications).<br> |
|StorageType |String |No |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total specifications. |
|InstanceSpecs |Array of [InstanceSpecObject](https://docs.byteplus.com/en/docs/61/15766#instancespecobject) |Refer to the sample response. |Specification list. |

### InstanceSpecObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Connection |Integer |200 |Max connections supported by the corresponding specification instance. |
|DBEngineVersion |String |PostgreSQL_14 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。<br><br><br>> **tip**<br><br><br>> The DBEngineVersion field is included in the returned InstanceSpecObject only when the DBEngineVersion field is specified in the DescribeDBInstanceSpecs request parameter.<br> |
|Memory |Integer |5 |Memory size. Unit is GB. |
|RegionId |String |cn\-beijing |Supported region ID. |
|SpecCode |String |rds.postgres.1c2g |instance specification code. |
|SpecStatus |String |Normal |Selling status of the specification in the availability zone, including the following:<br><br><br>* `Normal`: available for sale.<br><br>* `Soldout`: sold out. |
|VCPU |Integer |1 |CPU size. For example: 1 indicates 1U. |
|ZoneId |String |cn\-beijing\-a |Supported availability zone ID.<br><br>> **tip**<br><br><br>> The ZoneId field is returned in the InstanceSpecObject only when the ZoneId parameter is specified in the DescribeDBInstanceSpecs request.<br> |
|StorageType |String |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|StorageSpaceMax |Integer |3000 |The maximum storage space supported by the current specification, in GB. |
|StorageSpaceMin |Integer |20 |The minimum storage space supported by the current specification, unit is GB. |

## Example

### Sample request

```json
POST /?Action=DescribeDBInstanceSpecs&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250306201757BC8FEB1DB34377BC4F97-8e3f5c",
        "Action": "DescribeDBInstanceSpecs",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceSpecs": [
            {
                "Connection": 200,
                "Memory": 2,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.1c2g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 1
            },
            {
                "Connection": 400,
                "Memory": 4,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.2c4g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 2
            },
            {
                "Connection": 600,
                "Memory": 8,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.2c8g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 2
            },
            {
                "Connection": 1600,
                "Memory": 16,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.2c16g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 2
            },
            {
                "Connection": 800,
                "Memory": 8,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.4c8g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 4
            },
            {
                "Connection": 1600,
                "Memory": 16,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.4c16g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 4
            },
            {
                "Connection": 3200,
                "Memory": 32,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.4c32g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 4
            },
            {
                "Connection": 1600,
                "Memory": 16,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.8c16g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 8
            },
            {
                "Connection": 3200,
                "Memory": 32,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.8c32g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 8
            },
            {
                "Connection": 6400,
                "Memory": 64,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.8c64g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 8
            },
            {
                "Connection": 3200,
                "Memory": 32,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.16c32g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 16
            },
            {
                "Connection": 6400,
                "Memory": 64,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.16c64g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 16
            },
            {
                "Connection": 12800,
                "Memory": 128,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.16c128g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 16
            },
            {
                "Connection": 12800,
                "Memory": 128,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.32c128g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 32
            },
            {
                "Connection": 25600,
                "Memory": 256,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.postgres.32c256g",
                "SpecStatus": "Normal",
                "StorageSpaceMax": 3000,
                "StorageSpaceMin": 20,
                "StorageType": "LocalSSD",
                "VCPU": 32
            }
        ],
        "Total": 15
    }
}
```
