---
title: "DescribeRegions"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRegions"
---

Call the DescribeRegions to query the available geographical resources of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRegions&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

None.

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Regions |Array of [RegionObject](https://docs.byteplus.com/en/docs/265/57339#regionobject) |Refer to the Sample response. |Region list. |


<span id="regionobject"></span>
### RegionObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Description |String |China (Beijing) |Region description. |
|RegionId |String |cn\-beijing |Region ID. |
|RegionName |String |cn\-beijing |Region name. |
|Status |String |Available |Region state. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
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
        "RequestId": "20241108161312F27FDAB3CA3C4CA5****-c62332",
        "Action": "DescribeRegions",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Regions": [
            {
                "Description": "Asia Pacific (Johor)",
                "RegionId": "ap-southeast-1",
                "RegionName": "ap-southeast-1",
                "Status": "Available"
            },
            {
                "Description": "Asia Pacific (Jakarta)",
                "RegionId": "ap-southeast-3",
                "RegionName": "ap-southeast-3",
                "Status": "Available"
            },
            {
                "Description": "China (Hong Kong",
                "RegionId": "cn-hongkong",
                "RegionName": "cn-hongkong",
                "Status": "Available"
            }
        ]
    }
}
```


<span id="7zAdv7Tk"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
