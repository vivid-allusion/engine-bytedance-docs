---
title: "DescribeDBInstanceProxyParameters"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceProxyParameters"
---

Call the DescribeDBInstanceProxyParameters API to query the connection parameter configuration after read\-write separation is enabled on the default endpoint of an instance.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-0af11cd4\*\*\*\* |Instance ID. |
|ParameterName |String |No |ReadWriteProxyConnection |Proxy\-related parameters for the connection endpoint after enabling read/write separation.<br><br>> **tip**<br><br><br><br>* > Currently only supports the value ReadWriteProxyConnection, which refers to the number of connections parameter.<br><br><br>* > The parameter default value is empty. When set to empty, the API return value is also empty.<br> |
|EndpointId |String |No |postgres\-0af11cd4\*\*\*\*\-cluster |Connect endpoint ID.<br><br>> **tip**<br><br><br><br>* > The parameter default value is the ID of the instance's default endpoint.<br><br><br>* > Currently only supports passing the instance default endpoint ID.<br> |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-0af11cd4\*\*\*\* |Instance ID. |
|DBEngineVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|ParameterCount |String |1 |Number of parameters. |
|Parameters |Array of [ParameterObject](https://docs.byteplus.com/en/docs/61/45568#parameterobject) |Refer to the sample response. |Current running parameter list of this proxy. |

### ParameterObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CheckingCode |String |[on\|off] |Parameter value range. |
|DefaultValue |String |off |Parameter default value. Refers to the default value provided in the default template corresponding to this instance. |
|Description |String |Use EXPLAIN ANALYZE for plan logging. |Parameter description in English. |
|DescriptionZH |String |Enable the sampling of EXPLAIN ANALYZE output. |Parameter description in Chinese. |
|ForceRestart |Boolean |false |Restart or not takes effect, values: `true` or `false`. |
|Name |String |auto_explain.log_analyze |Parameter name. |
|Type |String |bool |Parameter value type. Values: `string`, `integer`, `real`, `bool`, and `enum`. |
|Value |String |off |Parameter value. Refers specifically to the current instance running value. |

## Sample

### Sample request

```json
POST /?Action=DescribeDBInstanceProxyParameters&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-f511b775****",
    "EndpointId": "postgres-f511b775****-cluster",
    "ParameterName": "ReadWriteProxyConnection"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025031919422828B3EE5B6F629AFF0F74-bb2104",
        "Action": "DescribeDBInstanceProxyParameters",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBEngineVersion": "PostgreSQL_17",
        "InstanceId": "postgres-f511b775****",
        "ParameterCount": "1",
        "Parameters": [
            {
                "CheckingCode": "[20-200]",
                "DefaultValue": "200",
                "Description": "After the endpoint opens the read-write split, the corresponding proxy connection number parameter.",
                "DescriptionZH": "终端开了读写分离后，其所对应的代理的连接数参数。",
                "ForceRestart": true,
                "Name": "ReadWriteProxyConnection",
                "Type": "integer",
                "Value": "20"
            }
        ]
    }
}
```
