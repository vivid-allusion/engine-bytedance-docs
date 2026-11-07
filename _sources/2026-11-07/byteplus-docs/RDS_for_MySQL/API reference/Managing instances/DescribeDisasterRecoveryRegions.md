---
title: "DescribeDisasterRecoveryRegions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedisasterrecoveryregions"
---

Call the DescribeDisasterRecoveryRegions API to view the list of regions where disaster recovery instances can be created.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this request parameter must be included. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Regions |Object[] |Please refer to the response example. |List of regions where disaster recovery instances can be created. |
|RegionId |String |cn\-beijing |Region ID. |
|RegionName |String |China North 2 (Beijing) |Region name. |

## Sample request

```json
POST /?Action=DescribeDisasterRecoveryRegions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202412052153480711DA3AB1992FA0CAD8-96c067",
        "Action": "DescribeDisasterRecoveryRegions",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-chongqing-sdv"
    },
    "Result": {
        "Regions": [
            {
                "RegionId": "ap-southeast-1",
                "RegionName": "华北 2 （北京）"
            },
            {
                "RegionId": "cn-shanghai",
                "RegionName": "华东 2 （上海）"
            },
            {
                "RegionId": "cn-guangzhou",
                "RegionName": "华南 1 （广州）"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
