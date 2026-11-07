---
title: "DescribeDBNodeParameterDifferences"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbnodeparameterdifferences"
---

Call the DescribeDBNodeParameterDifferences API to query the parameter differences between nodes of an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-25651c34\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|NodeDifferentParameters |Object[] |Refer to the response example. |List of node parameter differences. |
|ParameterName |String |bulk_insert_buffer_size |Parameter name. |
|NodeParameterValueDetails |Object[] |Please refer to the response example. |Details of the node difference parameters. |
|Expression |String |ibtmp1:50M:autoextend:max:30G |Parameter expression. |
|NodeId |String |mysql\-25651c34\*\*\*\*\-md1b4\-0 |Node ID. |
|NodeSpec |String |rds.mysql.d1.n.1c1g |Node specification. |
|NodeType |String |Primary |The master node needs to pass in `Primary`for NodeType, while the read\-only node does not need to pass it in. |
|ParameterValue |String |4194305 |Runtime value of the parameter. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |

## Sample request

```json
POST /?Action=DescribeDBNodeParameterDifferences&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-25651c34****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250605204036314B7292FA47816D6B56-561288",
        "Action": "DescribeDBNodeParameterDifferences",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-12"
    },
    "Result": {
        "NodeDifferentParameters": [
            {
                "NodeParameterValueDetails": [
                    {
                        "Expression": "",
                        "NodeId": "mysql-25651c34****-md1b4-0",
                        "NodeSpec": "rds.mysql.d1.n.1c1g",
                        "NodeType": "Primary",
                        "ParameterValue": "4194304",
                        "ZoneId": "ap-southeast-1-a"
                    },
                    {
                        "Expression": "",
                        "NodeId": "mysql-25651c34****-r399d",
                        "NodeSpec": "rds.mysql.d1.n.1c1g",
                        "NodeType": "ReadOnly",
                        "ParameterValue": "4194305",
                        "ZoneId": "ap-southeast-1-a"
                    }
                ],
                "ParameterName": "bulk_insert_buffer_size"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
