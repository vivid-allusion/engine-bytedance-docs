---
title: "DescribeAvailabilityZones"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones"
---

Call the DescribeAvailabilityZones API to query the list of availability zone resources of MongoDB in the specified region.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|RegionId |String |Yes |ap\-southeast\-1 |Region ID.<br><br>tip<br><br>You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/mongodb/describeregions) API to query the resource information for all available regions of a MongoDB instance, including the region ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|RegionId |String |ap\-southeast\-1 |Region ID. |
|Zones |Object[] | |A list of availability zones. |
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|ZoneName |String |Asia Pacific (Johor) \- Availability Zone A |Name of availability zone. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeAvailabilityZones&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "RegionId": "ap-southeast-1"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220221174244010225243118084C****",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RegionId": "ap-southeast-1",
        "Zones": [
            {
                "ZoneId": "ap-southeast-1a",
                "ZoneName": "ap-southeast-1a"
            }
        ]
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
