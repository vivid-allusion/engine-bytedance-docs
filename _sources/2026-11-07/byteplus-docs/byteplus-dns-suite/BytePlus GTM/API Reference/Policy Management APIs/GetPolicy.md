---
title: "GetPolicy"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/GetPolicy"
---

Gets the policy information of a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=GetPolicy&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetPolicy` |The name of the API. The value of this parameter is `GetPolicy`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`e93cb374-2b33-4202-842f-c066a4462c03` |The UUID of the GTM instance. You can obtain the `GtmId` through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PolicyType |String |Yes |`geo` |The policy type.<br><br><br>* geo: Basic routing.<br><br>* perf: Intelligent routing. |

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
|RoutingMode |String |The routing mode. This parameter can have the following values:<br><br><br>* lb: Based on load balancing, routes user traffic to different IDCs according to weight proportions.<br><br>* geo: Based on the user's geographical location and ISP, routes user traffic to the nearest IDC within the same ISP network.<br><br>* geo\-lb (default): First, based on the user's geographical location and ISP, routes user traffic to the access line of the nearest IDC within the same ISP network. Then, based on load balancing, routes user traffic to multiple IDCs according to proportions. |
|AlarmOnly |Boolean |Indicates whether BytePlus GTM only triggers an alarm notification without automatically switching to an available pool when the current pool set is unavailable. This parameter is only effective when `PolicyType` is set to `geo`. If `PolicyType` is set to `perf`, `AlarmOnly` is always `false`.<br><br><br>* true: BytePlus GTM only triggers an alarm notification.<br><br>* false: BytePlus GTM automatically switches to an available pool. |
|Targets |Array of Objects |The traffic targets of the intelligent routing policy. |
|PoolId |String |The pool ID. |
|Statistics |Objects |Statistical data for available and unavailable addresses. |
|InactiveAddr |Integer |The number of unavailable addresses. |
|ActiveAddr |Integer |The number of available addresses. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=GetPolicy&Version=2023-01-01&GtmId=e93cb374-2b33-4202-842f-c066a4462c03&PolicyType=perf
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023080711584012BFB041BDE2F044610C",
        "Action": "GetPolicy",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RoutingMode": "geo",
        "AlarmOnly": false,
        "Targets": [
            {
                "PoolId": "cf65f46e-6a19-4d15-99b5-684a6ce4e7ff"
            }
        ],
        "Statistics": {
            "InactiveAddr": 0,
            "ActiveAddr": 0
        }
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
