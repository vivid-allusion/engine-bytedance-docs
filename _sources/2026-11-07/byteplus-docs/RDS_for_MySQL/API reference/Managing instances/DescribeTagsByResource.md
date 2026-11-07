---
title: "DescribeTagsByResource"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetagsbyresource"
---

Call the ModifyDBEndpointDNS API to modify the resolution method of a private network address.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mysql\-46609cf2\*\*\*\*","mysql\-5564bc65\*\*\*\*"] |Instance ID. |
|TagFilters |Object[] |No |See the request example. |An array of tag key\-value pairs used for query filtering.<br><br>tip<br><br>A maximum of 10 tag key\-value pairs can be passed at a time for query filtering. |
|Key |String |Yes |ExampleKey |The tag key used for query filtering. |
|Value |String |No |ExampleValue |The tag value used for query filtering.<br><br>tip<br><br>If a tag value was set when binding the tag, this parameter is required during filtering. |
|Values |String[] |No |["ExampleValue1","ExampleValue2"] |The tag value used for query filtering.<br><br>tip<br><br>If both Value and Values are present, Values takes precedence. |
|PageNumber |Integer |Yes |1 |Current page number. The minimum value is 1. |
|PageSize |Integer |Yes |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 100. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |2 |Total number of tags. |
|TagResources |Object[] |See the response example. |The list of tags for the instance. |
|InstanceId |String |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|Key |String |table1 |The key of the tag bound to the instance. |
|Value |String |table2 |The value of the tag bound to the instance. |

## Sample request

```json
POST /?Action=DescribeTagsByResource&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-46609cf2****",
        "mysql-5564bc65****"
    ],
    "TagFilters": [
        {
            "Key": "test1"
        }
    ],
    "PageNumber": 1,
    "PageSize": 10
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308091903447828DBC85919F18E0646",
        "Action": "DescribeTagsByResource",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TagResources": [
            {
                "InstanceId": "mysql-46609cf2****",
                "Key": "test1",
                "Value": "123"
            },
            {
                "InstanceId": "mysql-5564bc65****",
                "Key": "test1",
                "Value": "123"
            }
        ],
        "Total": 2
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
