---
title: "DeletePool"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/DeletePool"
---

Deletes a pool.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=DeletePool&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DeletePool` |The name of the API. The value of this parameter is `DeletePool`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`5c7f5265-ca0f-4a60-bcd6-c4db7fcc4a95` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PoolId |String |Yes |`e462d15f-cfba-4dd3-a42b-9c2a7c2d0e1b` |You can get the ID of the pool from the [CreatePool API](https://docs.byteplus.com/docs/byteplus-dns-suite/CreatePool) or the [ListPools API](https://docs.byteplus.com/docs/byteplus-dns-suite/ListPools). |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

## Example

### Request example

```JSON
POST https://gtm.byteplusapi.com/?Action=DeletePool&Version=2023-01-01

{
   "GtmId": "2a8f91c4-aa07-4ae4-9ebc-68750d611822",
   "PoolId": "cf65f46e-6a19-4d15-99b5-684a6ce4e7ff"
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230727152318D60DAA2A8AF0E65F9619",
        "Action": "DeletePool",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
