---
title: "DescribeVortexIPsBilling"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPsBilling"
---

Call the DescribeVortexIPsBilling API to view billing information for Vortex IPs.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeVortexIPsBilling |The action that you want to perform. Value: DescribeVortexIPsBilling. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|PageNumber |Integer |No |1 |The page number of the list. Default: 1. |
|PageSize |Integer |No |20 |The number of entries per page in a pagination query. Value range: 1–100. Default: 10. |
|VortexIds.N |String |No |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) API to query the ID of the Vortex IP.<br><br><br>* N represents the sequence number of a Vortex IP ID. You can call a maximum of 20 IDs in a single request.<br><br>* Separate multiple IDs with ampersands (&). |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |Request ID. |
|TotalCount |Integer |33 |Number of Vortex IPs that meet the conditions. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |20 |Number of entries per page in the current pagination. |
|VortexIPBillingConfigs |Array of struct |\- |Details of a Vortex IP. For details, see the table: **VortexIP structure**. |


**VortexIP structure**


|Parameter name |Type |Example |Description |
|---|---|---|---|
|VortexId |String |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP. |
|BillingType |Integer |3 |Billing method.<br><br><br>* 1: Subscription.<br><br>* 3: Pay\-as\-you\-go |
|InstanceStatus |Integer |1 |Billing status of a Vortex IP.<br><br><br>* 0: Creating<br><br>* 1: Running<br><br>* 2: Creation failed<br><br>* 3: Unsubscribed<br><br>* 4: Suspended due to expiration<br><br>* 5: Reclaimed due to expiration<br><br>* 6: Suspended due to overdue payments<br><br>* 7: Reclaimed due to overdue payments<br><br>* 8: Suspended due to unsubscription |
|OverdueTime |String |2024\-04\-29T01:37:38Z |The time when the resource is overdue suspended. This parameter returns a value only if the resource is suspended due to overdue payments. |
|ReclaimTime |String |2024\-04\-29T01:37:38Z |The time when the resource is reclaimed forcibly. This parameter returns a value only when the resource is suspended due to overdue payments. |
|ExpiredTime |String |2024\-04\-29T01:37:38Z |The time when the Vortex IP expires. |
|OverdueReclaimTime |String |2024\-04\-29T01:37:38Z |The time when the Vortex IP is reclaimed due to expiration.<br><br> |
|RemainRenewTimes |Integer |1 |Number of remaining renewals available to the Vortex IP |
|RenewPeriodTimes |Integer |5 |Number of renewals for the Vortex IP.<br><br> |
|RenewType |Integer |2 |Renewal type of the Vortex IP.<br><br><br>* 1: Manual renewal.<br><br>* 2: Automatic renewal. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=DescribeVortexIPsBilling&Version=2020-04-01&AllocationId=eip-2ze7ujxscd**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "20210811152539010225146063030****",
        "Action": "DescribeVortexIPsBilling",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },   
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "VortexIPBillingConfigs": [
            {
                "VortexId": "vt-bp1o94dp5i6ea****",
                "BillingType": 1,
                "InstanceStatus": 1,
                "OverdueTime": "2024-04-29T01:37:38Z",
                "ReclaimTime": "2024-04-29T01:37:38Z",
                "ExpiredTime":"2024-04-29T01:37:38Z",
                "OverdueReclaimTime":"2024-04-29T01:37:38Z",
                "RemainRenewTimes":1,
                "RenewPeriodTimes":5,
                "RenewType":2
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/gavi-sept-test1/Public_error_codes).


|HttpCode |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format of specified pagination parameter is invalid. |
|400 |LimitExceeded.VortexIPNumber |You've reached the limit on the number of VortexIPs that you can operate. |The maximum that you can operate in a single request has been reached. |
