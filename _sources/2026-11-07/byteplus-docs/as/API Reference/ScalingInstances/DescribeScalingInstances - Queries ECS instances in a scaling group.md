---
title: "DescribeScalingInstances - Queries ECS instances in a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeScalingInstances"
---

Query instance information in a scaling group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScalingInstances&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|925ASG">必选</span> `Sample value: DescribeScalingInstances`

The operation you want to perform. Valid value: DescribeScalingInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|x5s6Z0">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span>`Optional` `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**CreationType ** <span data-label="purple">string </span>`Optional` `Sample value: AutoCreated`

The instance creation method. Valid values:


* AutoCreated: The instance is automatically created by the scaling group based on the instance configuration.

*  Attached: The instance is manually added to the scaling group.



**InstanceIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: i-ybmike5l70l8j1ha****`

The list of instance IDs. You can call [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) to query instance IDs.


* Parameter \- N: Specifies the serial number of the scaling group. Valid value: 1\-20.


Separate multiple instance IDs with &.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the list. The default value is 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–100. Default value: 10.



**ScalingConfigurationId ** <span data-label="purple">string </span>`Optional` `Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID. You can call [DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) to query the scaling configuration ID.



**Status ** <span data-label="purple">string </span>`Optional` `Sample value: InService`

The instance status. Valid values:


* Init: Initializing.

* Pending: Joining.

* Pending:Wait: Join pending.

* InService: In service.

* Error: Error.

* Removing: Removing.

* Removing:Wait: Removal pending.

* Stopped: Stopped.

* Protected: Protected.

* Standby: Standby.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**ScalingInstances ** <span data-label="purple">object[] </span>`Sample value: --`

The information about instances that meet the conditions.


**CreatedTime ** <span data-label="purple">string </span>`Sample value: 2022-04-02T16:00:00Z`

The time when the instance joined the scaling group, accurate to the second.



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybmike5l70l8j1ha****`

The instance ID.



**ScalingConfigurationId ** <span data-label="purple">string </span>`Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID.



**ScalingGroupId ** <span data-label="purple">string </span>`Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group to which the instance belongs.



**ScalingPolicyId ** <span data-label="purple">string </span>`Sample value: sp-ybmvamf8uql8j1fl****`

The scaling rule ID. A return value is provided only for instances automatically created based on scaling rules.



**Entrusted ** <span data-label="purple">boolean </span>`Sample value: true`

Specifies whether the instance is managed by the scaling group when an instance is added to a scaling group. Value:


* true: enable the scaling group to manage the lifecycle of an instance when the instance is added to the scaling group.

* false: does not enable the scaling group to manage the lifecycle of an instance when the instance is added to the scaling group.



**ZoneId ** <span data-label="purple">string </span>`Sample value: cn-beijing-a`

The ID of the availability zone to which the instance belongs.



**Status ** <span data-label="purple">string </span>`Sample value: InService`

The instance status. Valid value:


* Init: Initializing.

* Pending: Joining.

* Pending:Wait: Join pending.

* InService: In service.

* Error: Error.

* Removing: Removing.

* Removing:Wait: Removal pending.

* Stopped: Stopped.

* Protected: Protected.



**LaunchTemplateId ** <span data-label="purple">string </span>`Sample value: lt-yc5kwj1di33uw1qj****`

The ID of the instance launch template.



**CreationType ** <span data-label="purple">string </span>`Sample value: AutoCreated`

The instance creation method. Valid values:


* AutoCreated: The instance is automatically created based on the scaling configuration.

* Attached: The instance is manually added to the scaling group.



**LaunchTemplateVersion ** <span data-label="purple">string </span>`Sample value: Default`

The version of the instance launch template. Valid values:


* Default: The template's default version is always used.

* Latest: The template's latest version is always used.

* Other values: A specific template version number is used.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when a value is specified for the LaunchTemplateId parameter.</div>





**TotalCount ** <span data-label="purple">integer </span>`Sample value: 20`

The total number of instances that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScalingInstances&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112629Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507192632154165224230E09C6E",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "ScalingInstances": [
      {
        "CreatedTime": "2022-04-02T16:00:00Z",
        "InstanceId": "i-ybmike5l70l8j1ha****",
        "ScalingConfigurationId": "scc-ybmt16auaugh9zfy****",
        "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****",
        "ScalingPolicyId": "sp-ybmvamf8uql8j1fl****",
        "CreationType": "AutoCreated",
        "Entrusted": true,
        "ZoneId": "cn-beijing-a",
        "Status": "InService",
        "LaunchTemplateId": "lt-yc5kwj1di33uw1qj****",
        "LaunchTemplateVersion": "Default"
      }
    ],
    "TotalCount": 20
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidInstanceIds.Malformed |The specified amount of InstanceIds is malformed. |The number of specified instance IDs exceeds the upper limit. |
|400 |InvalidInstanceStatus |The specified Status is unsupported. |The specified instance status is not supported. |
|400 |InvalidInstanceCreationType |The specified CreationType is unsupported. |The specified instance creation method is not supported. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
