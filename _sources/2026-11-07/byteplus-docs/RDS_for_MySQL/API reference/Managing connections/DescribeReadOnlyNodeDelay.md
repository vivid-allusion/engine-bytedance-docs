---
title: "DescribeReadOnlyNodeDelay"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describereadonlynodedelay"
---

Call the DescribeReadOnlyNodeDelay API to query the delayed replication configuration of a read\-only node.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-3fb9a5be\*\*\*\* |The instance ID of the instance to which the read\-only node to be queried belongs. |
|NodeId |String |Yes |mysql\-3fb9a5be\*\*\*\*\-r3e01 |The node ID of the read\-only node to be queried. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|DelayReplicationTime |Long |1000 |The data delay time of the read\-only node, ranging from 1 to 604800, in seconds. A value of 0 indicates that the delayed replication feature is disabled. |
|NodeId |String |mysql\-3fb9a5be\*\*\*\*\-r3e01 |The node ID of the read\-only node to be queried. |

## Sample request

```json
POST /?Action=DescribeReadOnlyNodeDelay&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-3fb9a5be****",
    "NodeId": "mysql-3fb9a5be****-r3e01"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202312251448367989AF4644F5D756345E",
        "Action": "DescribeReadOnlyNodeDelay",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "DelayReplicationTime": 1,
        "NodeId": "mysql-3fb9a5be****-r3e01"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
