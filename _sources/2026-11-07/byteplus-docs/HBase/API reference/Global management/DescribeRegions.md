---
title: "DescribeRegions"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeRegions"
---

Call the DescribeRegions interface to query the available regional resource information of the HBase.

<span id="KTVxz1cX"></span>
## Request type

Synchronous request.

<span id="kyW4wHc5"></span>
## Request parameters

Empty.

<span id="SZ4rPkkK"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|Regions |Array of [Region](https://docs.byteplus.com/en/docs/219/60840#yVSvyobq) |Please refer to the request example. |List of regional information. |


<span id="yVSvyobq"></span>
### Region


|Name |Type |Example |Description |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Region ID. |
|RegionName |String |Asia Pacific (Johor) |Geographical name. |


<span id="fq6kXbBY"></span>
## Sample request

```json
POST /?Action=DescribeRegions&Version=2018-01-01 HTTP/1.1
Host: hbase.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "RegionId": "ap-southeast-1"
}
```


<span id="ALsUCjzy"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202204151506390101940591001265****",
        "Action": "DescribeRegions",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Regions": [
            {
                "RegionId": "ap-southeast-1",
                "RegionName": "Asia Pacific (Johor)"
            }
        ]
    }
}
```
