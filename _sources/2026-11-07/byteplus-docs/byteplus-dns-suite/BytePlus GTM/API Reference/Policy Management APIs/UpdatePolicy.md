---
title: "UpdatePolicy"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/UpdatePolicy"
---

Updates the policy of a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=UpdatePolicy&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePolicy` |The name of the API. The value of this parameter is `UpdatePolicy`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PolicyType |String |Yes |`geo` |The type of policy you need to update.<br><br><br>* geo: Basic routing.<br><br>* perf: Intelligent routing. |
|Policy |Object |Yes | |Policy parameters. |
|RoutingMode |String |No |`lb` |The routing mode. This parameter can have the following values:<br><br><br>* lb: Based on load balancing, routes user traffic to different IDCs according to weight proportions.<br><br>* geo: Based on the user's geographical location and ISP, routes user traffic to the nearest IDC within the same ISP network.<br><br>* geo\-lb (default): First, based on the user's geographical location and ISP, routes user traffic to the access line of the nearest IDC within the same ISP network. Then, based on load balancing, routes user traffic to multiple IDCs according to weight proportions. |
|AlarmOnly |Boolean |No |`true` |Indicates whether BytePlus GTM only triggers an alarm notification without automatically switching to an available pool when the current pool set is unavailable. This parameter is only effective when `PolicyType` is set to `geo`.<br><br><br>* true: BytePlus GTM only triggers an alarm notification.<br><br>* false: (default) BytePlus GTM automatically switches to an available pool. |
|Targets |Array of Objects |No | |The traffic targets of the intelligent routing policy. |
|PoolId |String |No |`cf65f46e-6a19-4d15-99b5-684a6ce4e7ff` |The pool ID. |
|PerfMode |String |No |`perf` |The routing mode for the intelligent routing policy. This parameter can have the following values:<br><br><br>* perf: Performance priority mode.<br><br>* cap\-perf: Capacity priority mode.<br><br><br>This parameter is only effective when the `PolicyType` parameter is set to `perf`. |

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
POST https://gtm.byteplusapi.com/?Action=UpdatePolicy&Version=2023-01-01

{
    "GtmId": "2a8f91c4-aa07-4ae4-9ebc-68750d611822",
    "PolicyType": "perf",
    "Policy": {
        "Targets": [
            {
                "PoolId": "cf65f46e-6a19-4d15-99b5-684a6ce4e7ff"
            }
        ]
    }
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "UpdatePolicy",
        "Region": "ap-southeast-1",
        "RequestId": "20210707160124010225145152005CF007",
        "Service": "gtm",
        "Version": "2023-01-01"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
