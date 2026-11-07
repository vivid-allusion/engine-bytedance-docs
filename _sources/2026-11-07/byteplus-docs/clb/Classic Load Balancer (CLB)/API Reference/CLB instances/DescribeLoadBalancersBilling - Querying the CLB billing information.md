---
title: "DescribeLoadBalancersBilling - Querying the CLB billing information"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancersBilling"
---

Call the DescribeLoadBalancersBilling API to query the billing information of the specified CLB instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeLoadBalancersBilling&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|atVje9">必选</span>`Example: DescribeLoadBalancersBilling`

Action to execute. Set the value to **DescribeLoadBalancersBilling**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|DcHkZU">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerIds.N ** <span data-label="purple">String </span>`optional` `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB instance ID.


* Parameter \- N: Represents the serial number of the CLB instance ID, ranging from 1 to 20.

* Connect multiple CLB instance IDs with ampersands (&).



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

Total number of instances that meet the conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The number of rows on the current page.



**LoadBalancerBillingConfigs ** <span data-label="purple">Object[] </span>`Example: -`

Billing configuration of the CLB instance.


**LoadBalancerId ** <span data-label="purple">String </span>`Example: clb-bp1b6c719dfa08ex****`

CLB instance ID.



**BillingType ** <span data-label="purple">Integer </span>`Example: 2`

Billing method of the CLB instance.


* 1: Subscription

* 2: Pay\-by\-Specification

* 3: Pay\-by\-CU


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pay\-by\-CU is currently in Beta stage and temporarily only supports accounts that have completed enterprise certification to apply for trial. If you need a trial, please contact your account manager.</div>




**RenewType ** <span data-label="purple">Integer </span>`Example: 2`

Renewal type of the CLB instance.


* 1: Manual renewal

* 2: Automatic renewal.

* 3: Non\-renewal upon expiration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned when <code>BillingType</code> is set to 1.</div>




**RenewPeriodTimes ** <span data-label="purple">Integer </span>`Example: 1`

The duration of a single auto\-renewal.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>RenewType</code> is 1 or 3, this parameter returns 0.</div>




**RemainRenewTimes ** <span data-label="purple">Integer </span>`Example: -1`

The number of automatic renewals available. The value can be \-1 or an integer from 1 to 100. A value of \-1 indicates unlimited auto\-renewal attempts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>RenewType</code> is 1 or 3, this parameter returns \-1.</div>




**InstanceStatus ** <span data-label="purple">Integer </span>`Example: 1`

Billing status of the CLB instance.


* 0: Creating

* 1: Running

* 2: Creation failed

* 3: Unsubscribed

* 4: Expired and suspended

* 5: Expired and reclaimed

* 6: Suspended due to overdue payments

* 7: Reclaimed due to overdue payments

* 8: Suspended due to unsubscription



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2021-08-11T23:59:59Z`

Expiration time of the CLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned when <code>BillingType</code> is set to 1.</div>




**ReclaimTime ** <span data-label="purple">String </span>`Example: 2021-08-26T23:59:59Z`

Reclaim time after expiration for a CLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned when <code>BillingType</code> is set to 1.</div>




**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

The suspension time of the CLB instance due to overdue payment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>BillingType</code> is 2 or 3, this parameter returns.</div>




**OverdueReclaimTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Reclaim time after the CLB instance is shut down due to overdue payment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>BillingType</code> is 2 or 3, this parameter returns.</div>





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeLoadBalancersBilling&Version=2020-04-01&LoadBalancerIds.1=clb-bp1b6c719dfa08ex****&PageNumber=1&PageSize=10
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLoadBalancersBilling",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "LoadBalancerBillingConfigs": [
            {
                "RenewType": 2,
                "BillingType": 2,
                "ExpiredTime": "2021-08-11T23:59:59Z",
                "OverdueTime": "2021-08-11T16:37:37Z",
                "ReclaimTime": "2021-08-26T23:59:59Z",
                "InstanceStatus": 1,
                "LoadBalancerId": "clb-bp1b6c719dfa08ex****",
                "RemainRenewTimes": -1,
                "RenewPeriodTimes": 1,
                "OverdueReclaimTime": "2021-08-11T16:37:37Z"
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "20210811152539010225146063030****",
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidPageNumber.Malformed |The specified PageNumber is malformed. |The specified PageNumber parameter format is invalid. |
|400 |InvalidPageSize.Malformed |The specified PageSize is malformed. |The format of the specified PageSize parameter is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceeded.LoadBalancerIdNumber |You've reached the limit on the number of description LoadBalancer that you can operate. |The maximum number of Load Balancers allowed for a single query has been reached. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
