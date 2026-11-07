---
title: "GetPool"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/GetPool"
---

Gets information of a pool of a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=GetPool&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetPool` |The name of the API. The value of this parameter is `GetPool`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PoolId |String |No |`7cd0ccd6-eeac-4db8-9076-ca297cf8df75` |ID of the pool. You can get the ID of the pool from the [CreatePool API](https://docs.byteplus.com/docs/byteplus-dns-suite/CreatePool) or the [ListPools API](https://docs.byteplus.com/docs/byteplus-dns-suite/ListPools). The default is an empty value, meaning this parameter is not used as a query condition. |

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
|CreateTime |String |Creation time of the pool. Accurate to milliseconds. The format complies with the ISO 8601 standard. |
|UpdateTime |String |Most recent modification time of the pool. Accurate to milliseconds. The format complies with the ISO 8601 standard. |
|PoolId |String |ID of the pool. |
|Name |String |Name of the pool. |
|Remark |String |Remark of the pool. |
|Addresses |Array of Objects |Addresses in the pool. |
|Value |String |Address. |
|Weight |Integer |Weight of the address.<br><br> <br><br>For addresses without a set weight value, this parameter returns the default weight value of 1. |
|Capacity |Integer |Capacity of the address.<br><br> <br><br>For addresses without a set capacity value, this parameter returns the default capacity value of 1000. |
|RectifiedGeos |Array of Strings |Corrected address belonging area. |
|Mode |String |Mechanism for determining whether the address is available.<br><br><br>* auto: Automatic mode. Cloud scheduling determines whether the address is available based on the health check results.<br><br>* always_on: The address is always available.<br><br>* always_off: The address is always unavailable. |
|Geo |String |Default belonging area of the address. |
|AddrType |String |Type of address in the pool.<br><br><br>* ip4: IPv4 address.<br><br>* ip6: IPv6 address.<br><br>* host: Domain name, e.g., www.example.com. |
|Capacity |Integer |Capacity of the pool. If the addresses in the pool do not have a set capacity, this parameter returns the default capacity value of 1000. |
|CapacityMode |String |In capacity or load feedback routing mode, choose to configure the capacity of the pool or the address.<br><br><br>* address: Configure the capacity of the address. When you select address, you can only set the Capacity parameter for each address. The value of the pool Capacity parameter is automatically summed from the values of the address Capacity, and you cannot modify it. In load feedback routing mode, you can only report the capacity and load of the address.<br><br>* pool: Configure the capacity of the pool. When you select pool, you can only set the Capacity parameter of the pool. The value of the Capacity parameter for each address is automatically averaged from the value of the Capacity parameter of the pool. You cannot modify it. In load feedback routing mode, you can only report the capacity and load of the pool. |
|Deletable |Boolean |Whether the pool can be deleted.<br><br><br>* true: The pool is not referenced by any rules and can be deleted.<br><br>* false: The pool is referenced by one or more rules and cannot be deleted. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=GetPool&Version=2023-01-01&GtmId=2a8f91c4-aa07-4ae4-9ebc-68750d611822&PoolId=cf65f46e-6a19-4d15-99b5-684a6ce4e7ff
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024060620113734D1D01CDFC1B6003159",
        "Action": "GetPool",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "CreateTime": "2024-06-06T11:25:50.051Z",
        "UpdateTime": "2024-06-06T11:25:50.051Z",
        "PoolId": "7cd0ccd6-eeac-4db8-9076-ca297cf8df75",
        "Name": "example",
        "Remark": "",
        "Addresses": [
            {
                "Value": "1.*.*.*",
                "Weight": 1,
                "Capacity": 1000,
                "Mode": "auto",
                "Geo": "Oceania_Australia"
            }
        ],
        "AddrType": "ipv4",
        "Capacity": 100,
        "CapacityMode": "address",
        "Deletable": false
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
