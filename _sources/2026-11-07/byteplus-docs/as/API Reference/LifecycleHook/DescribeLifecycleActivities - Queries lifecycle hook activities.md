---
title: "DescribeLifecycleActivities - Queries lifecycle hook activities"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeLifecycleActivities"
---

Query lifecycle hook activities.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeLifecycleActivities&groupName=%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%8C%82%E9%92%A9&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|fSMcek">必选</span> `Sample value: DescribeLifecycleActivities`

The action that you want to perform. Value: DescribeLifecycleActivities.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|dMJ5Fu">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span>`Optional` `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**LifecycleHookIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook. You can call [DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks)  to query the lifecycle hook ID.


* Parameter \- N: Indicates the serial number of the lifecycle hook. Value: 1–10.

* Separate multiple lifecycle hook IDs with &.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: i-ybmike5l70l8j1ha****`

The instance ID. This parameter is used to query the detailed lifecycle hook activity related to the specified instance. You can call [DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) to query the instance ID in the specified scaling group.



**LifecycleActivityStatus ** <span data-label="purple">string </span>`Optional` `Sample value: Pending`

The status of the lifecycle hook activity. Valid values:


* Pending: Suspended status.

* Timeout: For the target lifecycle hook activity, the timeout period specified by the associated lifecycle hook has been reached, and the suspended status of the ECS instance ends automatically.

* Completed: The lifecycle hook activity is complete. This indicates the suspended status of the ECS instance has been manually ended.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the list. The default value is 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–100. Default value: 10.



**ScalingActivityId ** <span data-label="purple">string </span>`Optional` `Sample value: sga-ybn0mwfy1yl8j1f6****`

The ID of the scaling log. You can call [DescribeScalingActivities](https://docs.byteplus.com/en/docs/as/DescribeScalingActivities) to query the scaling log ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LifecycleActivities ** <span data-label="purple">object[] </span>`Sample value: --`

Information on lifecycle hook activities that meet the conditions.


**LifecycleActivityId ** <span data-label="purple">string </span>`Sample value: sgha-ybw2idr7kogsnzd9****`

The ID of the lifecycle hook activity.



**ScalingActivityId ** <span data-label="purple">string </span>`Sample value: sga-ybn0mwfy1yl8j1f6****`

The ID of the scaling log.



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybmike5l70l8j1ha****`

The ID of the ECS instance associated with the lifecycle hook activity.



**LifecycleHookId ** <span data-label="purple">string </span>`Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook.



**LifecycleActivityStatus ** <span data-label="purple">string </span>`Sample value: Pending`

The status of the lifecycle hook activity. Valid values:


* Pending: Suspended status.

* Timeout: For the target lifecycle hook activity, the timeout period specified by the associated lifecycle hook has been reached, and the suspended status of the ECS instance ends automatically.

* Completed: The lifecycle hook activity is complete. This indicates the suspended status of the ECS instance has been manually ended.



**LifecycleHookPolicy ** <span data-label="purple">string </span>`Sample value: CONTINUE`

The execution policy after the lifecycle hook suspension ends. Valid values:


* CONTINUE: Execution continues.

* REJECT: Subsequent execution is discontinued.




**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 20`

The total number of lifecycle hook activities that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeLifecycleActivities&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T111923Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024050719193318316812906016C01E",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "LifecycleActivities": [
      {
        "LifecycleActivityId": "sgha-ybw2idr7kogsnzd9****",
        "ScalingActivityId": "sga-ybn0mwfy1yl8j1f6****",
        "InstanceId": "i-ybmike5l70l8j1ha****",
        "LifecycleHookId": "sgh-ybrzhc5ht08hccnm****",
        "LifecycleActivityStatus": "Pending",
        "LifecycleHookPolicy": "CONTINUE"
      }
    ],
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 20
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
