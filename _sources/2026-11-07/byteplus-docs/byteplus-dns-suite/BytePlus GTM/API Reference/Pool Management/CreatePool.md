---
title: "CreatePool"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/CreatePool"
---

Creates a pool for a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=CreatePool&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CreatePool` |The name of the API. The value of this parameter is `CreatePool`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|Pool |Object |Yes | |The pool. |
|Name |String |Yes |`Pool` |Name of the pool. In UTF\-8 format. The maximum length is 64 UTF\-8 characters. |
|Remark |String |No |`Remark` |Remark of the pool. The default is an empty string. In UTF\-8 format. The maximum length is 128 UTF\-8 characters. |
|AddrType |String |No |`ipv4` |Address type of the pool. If you do not set this parameter, BytePlus GTM will automatically determine the address type of the pool.<br><br><br>* ipv4: IPv4 address.<br><br>* ipv6: IPv6 address.<br><br>* cname: Domain name. |
|CapacityMode |String |No |`address` |In capacity or load feedback routing mode, choose to configure the capacity of the pool or the address.<br><br><br>* address (default): Configure the capacity of the address. When you select address, you can only set the Capacity parameter for each address. The value of the pool Capacity parameter is automatically summed from the values of the address capacity, and you cannot modify it. In load feedback routing mode, you can only report the capacity and load of the address.<br><br>* pool: Configure the capacity of the pool. When you select pool, you can only set the Capacity parameter of the pool. The value of the Capacity parameter for each address is automatically averaged from the value of the Capacity parameter of the pool. You cannot modify it. In load feedback routing mode, you can only report the capacity and load of the pool. |
|Capacity |Integer |No |`1000` |Capacity of the pool. The default is 1000. The value range is [1,100000].<br><br> <br><br>This parameter is only valid when the GTM instance policy is intelligent routing and the routing policy is capacity or load feedback. It is recommended to set a value in the range of [1000, 50000]. |
|Addresses |Array of Objects |Yes | |Addresses in the pool. |
|Value |String |Yes |`1.1.1.1` |Address. |
|Weight |Integer |No |`1` |Weight of the address. The default is 1. This parameter is only valid when the GTM instance policy is basic routing and load balancing is enabled. |
|Capacity |Integer |No |`1000` |Capacity of the address. The default is 1000. The value range is [1,100000].<br><br> <br><br>This parameter is only valid when the GTM instance policy is intelligent routing and the routing policy is capacity or load feedback. |
|RectifiedGeos |String[] |No |`["os_oceanica_au"]` |Corrected address belonging area. You need to fill in the line codes in this parameter. If you do not set this parameter, BytePlus GTM will not correct the belonging area. |
|Mode |String |No |`auto` |Mechanism for determining whether the address is available.<br><br><br>* auto (default): Automatic mode. BytePlus GTM determines whether the address is available based on the health check results.<br><br>* always_on: The address is always available.<br><br>* always_off: The address is always unavailable. |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|PoolId |String |ID of the pool. |

## Example

### Request example

```JSON
POST https://gtm.byteplusapi.com/?Action=CreatePool&Version=2023-01-01

{
   "GtmId": "2a8f91c4-aa07-4ae4-9ebc-68750d611822",
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

```json
{
    "ResponseMetadata": {
        "RequestId": "20230727152318D60DAA2A8AF0E65F9619",
        "Action": "CreatePool",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PoolId": "cf65f46e-6a19-4d15-99b5-684a6ce4e7ff"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
