---
title: "DescribeAvailabilityZones"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones"
---

Call the DescribeAvailabilityZones API to query the list of availability zones (AZs).

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The DescribeAvailabilityZones API routes requests based on the Region parameter in the Header. It only queries availability zone information for the region specified in the header and will not return information for other regions.

* Call the [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_PG/describeregions) API to query region information.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

None.

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID. |
|Zones |Array of [ZoneObject](https://docs.byteplus.com/en/docs/61/15758#zoneobject) |Refer to the sample response. |Availability zone list. |


<span id="zoneobject"></span>
### ZoneObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|ZoneName |String |cn\-beijing\-a |Availability zone name. |
|Description |String |China (Beijing) \- Availability zone A |Availability zone name within the region. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeAvailabilityZones&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "RegionID": "cn-beijing"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230801145904E960E37BE9C8BF1DD50F",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RegionId": "cn-beijing",
        "Zones": [
            {
                "Description": "华北2（北京）-可用区A",
                "ZoneId": "cn-beijing-a",
                "ZoneName": "cn-beijing-a"
            },
            {
                "Description": "华北2（北京）-可用区B",
                "ZoneId": "cn-beijing-b",
                "ZoneName": "cn-beijing-b"
            }
        ]
    }
}
```
