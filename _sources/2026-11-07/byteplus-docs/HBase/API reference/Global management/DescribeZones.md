---
title: "DescribeZones"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeZones"
---

Call the DescribeZones interface to query the availability zone resource information in the specified region of the HBase.

<span id="KIkTWtId"></span>
## Request type

Synchronous request.

<span id="yPz55caK"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|RegionId |String |Yes |ap\-southeast\-1 |Region ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeRegions">DescribeRegions</a> interface to query all available region resource information of the HBase instance, including the region ID.</div><br> |


<span id="PdqnKr2x"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|Zones |Array of [ZoneInfo](https://docs.byteplus.com/en/docs/219/60839#kRWxgkWo) |Please refer to the return example. |List of available zones. |


<span id="kRWxgkWo"></span>
### ZoneInfo


|Name |Type |Example |Description |
|---|---|---|---|
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|ZoneName |String |ap\-southeast\-1a |The name of the availability zone. |


<span id="q0HSSxz5"></span>
## Sample request

```json
POST /?Action=DescribeZones&Version=2018-01-01 HTTP/1.1
Host: hbase.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "RegionId": "ap-southeast-1"
}
```


<span id="RseazY3f"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202204151506390101940591001265****",
        "Action": "DescribeZones",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Zones": [
            {
                "ZoneId": "ap-southeast-1a",
                "ZoneName": "ap-southeast-1a"
            },
            {
                "ZoneId": "ap-southeast-1b",
                "ZoneName": "ap-southeast-1b"
            }
        ]
    }
}
```
