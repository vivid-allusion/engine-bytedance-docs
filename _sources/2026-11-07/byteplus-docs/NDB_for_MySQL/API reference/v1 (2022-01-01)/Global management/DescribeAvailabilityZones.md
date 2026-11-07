---
title: "DescribeAvailabilityZones"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones"
---

Call the DescribeAvailabilityZones to query the Availability Zone resources supported by the instance in the current region.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAvailabilityZones&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |No |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is left empty, information about availability zone resources in all available regions for the instance is returned.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRegions">DescribeRegions</a> API to query resource information in all available regions for the instance, including the Region ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID. |
|Zones |Array of [ZonesObject](https://docs.byteplus.com/en/docs/265/57340#zonesobject) |Refer to the Sample response. |Availability zone list. |


<span id="zonesobject"></span>
### ZonesObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|ZoneName |String |cn\-beijing\-a |Availability zone name. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeAvailabilityZones&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20220316122811010211173098010D****",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "RegionId": "cn-beijing",
        "Zones": [
            {
                "Description": "可用区A",
                "Status": "Normal",
                "ZoneId": "cn-beijing-a",
                "ZoneName": "cn-beijing-a"
            },
            {
                "Description": "可用区B",
                "Status": "Normal",
                "ZoneId": "cn-beijing-b",
                "ZoneName": "cn-beijing-b"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
