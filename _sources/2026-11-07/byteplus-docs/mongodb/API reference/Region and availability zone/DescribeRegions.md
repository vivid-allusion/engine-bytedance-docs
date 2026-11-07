---
title: "DescribeRegions"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describeregions"
---

Call the DescribeRegions API to query the available regional resource list of MongoDB.

## Request type

Synchronous request.

## Request parameters

None.

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |3 |Total number of region information entries. |
|Regions |Object[] | |Region information list. |
|RegionId |String |ap\-southeast\-1 |Region ID. |
|RegionName |String |Asia Pacific (Johor) |Region name. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202202211539050101742350380678****",
        "Action": "DescribeRegions",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Regions": [
            {
                "RegionId": "ap-southeast-1",
                "RegionName": "Asia Pacific (Johor)"
            }
        ],
        "Total": 1
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
