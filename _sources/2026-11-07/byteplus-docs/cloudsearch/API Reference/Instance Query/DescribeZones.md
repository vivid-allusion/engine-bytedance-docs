---
title: "DescribeZones"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeZones"
---

Call DescribeZones to query the Availability Zones where Cloud Search is available in a specified Region.

<span id="d9cac0c5"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=DescribeZones&Version=2023\-01\-01 HTTP/1.1


<span id="ba947c9a"></span>
## Request parameters

<span id="d88921b1"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DescribeZones` |The action that you want to perform. Value: `DescribeZones`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="15cda7cd"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |ap\-southeast\-1 |The ID of the Region to be queried. |


<span id="f3f54f3b"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Zones |Array of [Zones](https://docs.byteplus.com/docs/cloudsearch/DescribeZones#81966493) |/\- |The list of Availability Zones. |


<span id="81966493"></span>
### **Zones**


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |The Region ID. |
|ZoneId |String |ap\-southeast\-1a |The Availability Zone ID. |
|ZoneName |String |ap\-southeast\-1a |The name of the Availability Zone. |
|ZoneStatus |String |AVAILABLE |The status of the Availability Zone. |


<span id="3336d01b"></span>
## Sample request

```json
POST https://open.ap-southeast-1.byteplusapi.com/?Action=DescribeZones&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "RegionId": "ap-southeast-1"
}
```


<span id="ed35d4bf"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202310231017313****A60DADB80BE85",
        "Action": "DescribeZones",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Zones": [
            {
                "RegionId": "ap-southeast-1",
                "ZoneId": "ap-southeast-1a",
                "ZoneName": "ap-southeast-1a",
                "ZoneStatus": "AVAILABLE"
            }
        ]
    }
}
```
