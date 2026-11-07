---
title: "DescribeRegions"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describeregions"
---

Call the DescribeRegions API to query the list of available regions.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

None.

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Regions |Array of [RegionObject](https://docs.byteplus.com/en/docs/61/15759#regionobject) |Refer to the sample response. |Region list. |


<span id="regionobject"></span>
### RegionObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID. |
|RegionName |String |cn\-beijing |Region name. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080114393435F0D491F50B8A1BF16C",
        "Action": "DescribeRegions",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Regions": [
            {
                "RegionId": "cn-beijing",
                "RegionName": "cn-beijing"
            }
        ]
    }
}
```
