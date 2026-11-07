---
title: "UpdatePool"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/UpdatePool"
---

Updates a pool.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=UpdatePool&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePool` |The name of the API. The value of this parameter is `UpdatePool`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`5c7f5265-ca0f-4a60-bcd6-c4db7fcc4a95` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PoolId |String |Yes |`e462d15f-cfba-4dd3-a42b-9c2a7c2d0e1b` |You can get the ID of the pool from the [CreatePool API](https://docs.byteplus.com/docs/byteplus-dns-suite/CreatePool) or the [ListPools API](https://docs.byteplus.com/docs/byteplus-dns-suite/ListPools). |
|Pool |Object |Yes | |The pool. |
|Name |String |Yes |`Pool` |Name of the pool. In UTF\-8 format. The maximum length is 64 UTF\-8 characters. |
|Remark |String |No |`Remark` |Remark of the pool. In UTF\-8 format. The maximum length is 128 UTF\-8 characters. The default is an empty string. |
|AddrType |String |No |`ipv4` |Target address type of the pool. If you do not set this parameter, BytePlus GTM will automatically determine the address type of the pool.<br><br><br>* ipv4: IPv4 address.<br><br>* ipv6: IPv6 address.<br><br>* cname: Domain name. |
|CapacityMode |String |No |`address` |In capacity or load feedback routing mode, choose to configure the capacity of the pool or the address.<br><br><br>* address (default): Configure the capacity of the address. When you select address, you can only set the Capacity parameter for each address. The value of the pool Capacity parameter is automatically summed from the values of the address capacity, and you cannot modify it. In load feedback routing mode, you can only report the capacity and load of the address.<br><br>* pool: Configure the capacity of the pool. When you select pool, you can only set the Capacity parameter of the pool. The value of the Capacity parameter for each address is automatically averaged from the value of the Capacity parameter of the pool. You cannot modify it. In load feedback routing mode, you can only report the capacity and load of the pool. |
|Capacity |Integer |No |`1000` |Capacity of the pool. The default is 1000. The value range is [1,100000].<br><br> <br><br>This parameter is only valid when the GTM instance policy is intelligent routing and the policy is capacity or load feedback. It is recommended to set a value in the range of [1000, 50000]. |
|Addresses |Array of Objects |Yes | |Addresses in the pool. |
|Value |String |Yes |`1.1.1.1` |Address. |
|Weight |Integer |No |`1` |Weight of the address. The default is 1. This parameter is only valid when the GTM instance policy is basic routing and load balancing is enabled. |
|Capacity |Integer |No |`1000` |Capacity of the address. The default is 1000. The value range is [1,100000].<br><br> <br><br>This parameter is only valid when the GTM instance policy is intelligent routing and the policy is capacity. |
|RectifiedGeos |Array of Strings |No |`["os_oceanica_au"]` |Corrected address belonging area. You need to fill in the line codes in this parameter. If you do not set this parameter, BytePlus GTM will not correct the belonging area. |
|Mode |String |No |`auto` |Mechanism for determining whether the address is available.<br><br><br>* auto (default): Automatic mode. Cloud scheduling GTM determines whether the address is available based on the health check results.<br><br>* always_on: The address is always available.<br><br>* always_off: The address is always unavailable. |

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
POST https://gtm.byteplusapi.com/?Action=UpdatePool&Version=2023-01-01

{
    "GtmId": "5c7f5265-ca0f-4a60-bcd6-c4db7fcc4a95",
    "PoolId": "e462d15f-cfba-4dd3-a42b-9c2a7c2d0e1b",
    "Pool": {
        "Name": "example-pool",
        "Remark": "",
        "AddrType": "ipv4",
        "Addresses": [
            {
                "Value": "1.1.1.1",
                "Weight": 3,
                "RectifiedGeos": ["os_oceanica_au"],
                "Mode": "auto"
            }
        ]
    }
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230727152318D60DAA2A8AF0E65F9619",
        "Action": "UpdatePool",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
