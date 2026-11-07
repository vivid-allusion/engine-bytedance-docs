---
title: "DescribeRegions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions"
---

Call the DescribeRegions API to view the list of regions.

## Request type

Synchronous request.

## Request parameters

None.

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Regions |Object[] |{<br><br>"RegionId": "cn\-beijing",<br><br>"RegionName": "cn\-beijing"<br><br>} |List of regions. |
|RegionId |String |cn\-beijing |Region ID. |
|RegionName |String |China North 2 (Beijing) |Region name. |

## Sample request

```json
POST /?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202301092212492E5BD94BE9957BB3F409",
        "Action": "DescribeRegions",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Regions": [
            {
                "RegionId": "ap-southeast-1",
                "RegionName": "华北2（北京）"
            },
            {
                "RegionId": "cn-guangzhou",
                "RegionName": "华南1（广州）"
            },
            {
                "RegionId": "cn-shanghai",
                "RegionName": "华东2（上海）"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
