---
title: "DescribeScalingGroups - Queries the list of scaling groups"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeScalingGroups"
---

Obtain scaling group information. If there is no matching scaling group, the non\-matching item will be automatically ignored, and the query of other scaling groups will continue.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScalingGroups&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|9mlgr1">必选</span> `Sample value: DescribeScalingGroups`

The action that you want to perform. Value: DescribeScalingGroups.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|eXueUL">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the scaling group belongs.



**ScalingGroupIds.N ** <span data-label="purple">string[] </span>`可选` `Sample value: scg-ybmssdnnhn5pkgyd****`

The list of scaling group IDs.


* Parameter \- N: Specifies the serial number of the scaling group. Valid value: 1\-10.

* Separate multiple scaling group IDs with ampersands (&).



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`可选` Sample value`: k1`

The key of the tag.


* Parameter \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with &. Tag keys must be unique.



**TagFilters.N.Value ** <span data-label="purple">string[] </span>`可选` `Sample value: v1`

The user tag value.


* Parameter \- N: Specifies the serial number of the tag value. Value range: 1–20.

* Separate multiple tag values with &.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value specified when resources are queried based on tags. The first N specifies the serial number of the tag key. Value range: 1–10. The second N specifies the serial number of the tag value. Valid range: 1\-3. That is, you can query up to three tag values of the same tag key. \- Separate multiple tag values with &.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the list. The default value is 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–50. Default value: 10.



**ScalingGroupNames.N ** <span data-label="purple">string[] </span>`可选` `Sample value: scaling-group-1`

The name of the scaling group.


* Parameter \- N: Specifies the serial number of the scaling group. Valid value: 1\-10.

* Use & to separate multiple scaling group names.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**ScalingGroups ** <span data-label="purple">object[] </span>`Sample value: --`

Information on scaling groups that meet the conditions.


**ActiveScalingConfigurationId ** <span data-label="purple">string </span>`Sample value: scc-3u1mfze31u3dllw****`

The ID of the scaling configuration associated with the scaling group.



**ScalingGroupId ** <span data-label="purple">string </span>`String example: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



**DesireInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The expected number of instances running in the scaling group.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2022-04-10T18:29:38+08:00`

The creation time of the scaling group.



**MaxInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 100`

The maximum number of instances in the scaling group.



**MinInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 0`

The minimum number of instances in the scaling group.



**TotalInstanceCount ** <span data-label="purple">integer </span>`Sample value: 1`

The number of instances currently running in the scaling group.



**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2022-04-14T18:29:38+08:00`

The update time of the scaling group.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-2fevwte3frk0059gp67d6****`

The VPC ID of the scaling group.



**DBInstanceIds ** <span data-label="purple">string[] </span>`Sample value: rds-mysql-42b38c76****`

Information on RDS database associated with the scaling group.



**ServerGroupAttributes ** <span data-label="purple">object[] </span>`Sample value: --`

Information on Load Balancer associated with the scaling group.


**LoadBalancerId ** <span data-label="purple">string </span>`Sample value: clb-12augb3oetgxs17q7y24a****`

The Load Balancer ID.



**ServerGroupId ** <span data-label="purple">string </span>`Sample value: rsp-12b2z5fnxvhts17q7y2fj****`

The ID of the Load Balancer backend server group.



**Port ** <span data-label="purple">integer </span>`Sample value: 80`

The port number of servers in the Load Balancer backend server group.



**Weight ** <span data-label="purple">integer </span>`Sample value: 20`

The weight of the server in the Load Balancer backend server group.



**Type ** <span data-label="purple">string </span>`Sample value: CLB`

The type of Load Balancer. Valid values:


* CLB: Classic Load Balancer.

* ALB: Application Load Balancer.




**LifecycleState ** <span data-label="purple">string </span>`Sample value: Active`

Indicates the status of the scaling group. Valid values:


* Active: Enabled.

* InActive: Inactive.

* Deleting: Being deleted.

* Locked: Locked.

* CoolingDown: Cooling.

* Unknown: Unknown state.



**MultiAZPolicy ** <span data-label="purple">string </span>`Sample value: PRIORITY`

Scaling policy. Valid values:


* PRIORITY: Priority policy.

* BALANCE: Balanced distribution policy.


For details on subsequent instance scaling activities, refer to the "Scaling Policy" parameter description in [Creating scaling groups](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group).



**ScalingGroupName ** <span data-label="purple">string </span>`Sample value: scaling-group-test`

The name of the scaling group.



**DefaultCooldown ** <span data-label="purple">integer </span>`Sample value: 10`

The cooldown time of the scaling group.



**InstanceTerminatePolicy ** <span data-label="purple">string </span>`Sample value: NewestInstance`

The instance removal policy. Valid values:


* OldestInstance: Removes the instance that was added earliest (**automatically created or manually added**) to the scaling group.

* NewestInstance: Removes the instance that was added most recently (**automatically created or manually added**) to the scaling group.

* OldestScalingConfigurationWithOldestInstance (default): Removes the earliest instance **automatically created** in the scaling group based on the earliest scaling configuration of the group.

* OldestScalingConfigurationWithNewestInstance: Removes the most recently **created** instance in the scaling group based on the earliest scaling configuration of the group.



**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: subnet-24sdlkdplsjkdjd****`

The ID list of subnets of primary network interfaces of instances in the scaling group.



**LaunchTemplateId ** <span data-label="purple">string </span>`Sample value: lt-yc5kwj1di33uw1qj****`

The ID of the instance launch template.



**LaunchTemplateOverrides ** <span data-label="purple">object[] </span>`Sample value: --`

The information about the instance launch template.


**InstanceType ** <span data-label="purple">string </span>`Sample value: ecs.g2a.large`

Instance type.



**WeightedCapacity ** <span data-label="purple">integer </span>`Sample value: 1`

The weight of the instance type.



**PriceLimit ** <span data-label="purple">float </span>`Sample value: 0.001`

The maximum hourly price for the spot instance type.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A value of this parameter is returned only when the billing mode specified in the launch template is of the spot type with a price upper limit (which is SpotWithPriceLimit).</div>





**LaunchTemplateVersion ** <span data-label="purple">string </span>`Sample value: Default`

The version of the instance launch template. Valid values:


* Default: The template's default version is always used.

* Latest: The template's latest version is always used.

* Other values: A specific template version number is used.



**StoppedInstanceCount ** <span data-label="purple">integer </span>`Sample value: 10`

The number of disabled instances in the scaling group.



**HealthCheckType ** <span data-label="purple">string </span>`Sample value: ECS`

Indicates the health check method of the scaling group. Valid values:


* NONE: No health check for instances.

* ECS: Performs health check for ECS instances in the scaling group.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Tag information of the scaling group.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**ScalingMode ** <span data-label="purple">string </span>`Sample value: release`

The instance reclaim mode of the scaling group. Valid values:


* release: Release mode.

* recycle: Stop\-and\-reclaim mode.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project to which the scaling group belongs.



**InstancesDistribution ** <span data-label="purple">object </span>`Sample value: --`

Indicates the mixed configuration details of pay\-as\-you\-go instances and spot instances. This parameter is valid only when the specified billing method of the [scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources) associated with the scaling group is of the spot type.


**OnDemandBaseCapacity ** <span data-label="purple">integer </span>`Sample value: 0`

The minimum number of pay\-as\-you\-go instances in the scaling group.



**OnDemandPercentageAboveBaseCapacity ** <span data-label="purple">integer </span>`Sample value: 0`

Specifies the proportion of pay\-as\-you\-go instances after the minimum pay\-as\-you\-go instance count of the scaling group is met.



**CompensateWithOnDemand ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to allow using pay\-as\-you\-go instances to supplement spot instance capacity.



**SpotInstanceRemedy ** <span data-label="purple">boolean </span>`Sample value: false`

Indicates whether to allow replacing spot instances which are about to expire.




**LoadBalancerHealthCheckGracePeriod ** <span data-label="purple">integer </span>`Sample value: 60`

The grace period before CLB health check for instances in the scaling group.



**SuspendedProcesses ** <span data-label="purple">string[] </span>`Sample value: ScaleIn`

The paused process. If there are no paused processes, an empty value is returned. Valid values:


* ScaleIn: Scale\-in process.

* ScaleOut: Scale\-out process.

* HealthCheck: Health check.

* AlarmNotification: Alert task.

* ScheduledAction: Scheduled task.




**TotalCount ** <span data-label="purple">integer </span>`Sample value: 20`

The total number of scaling groups that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScalingGroups&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T093615Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507173729242176052105F626CE",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "ScalingGroups": [
      {
        "ActiveScalingConfigurationId": "scc-3u1mfze31u3dllw****",
        "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****\t",
        "InstanceTerminatePolicy": "NewestInstance",
        "DefaultCooldown": 10,
        "ScalingGroupName": "scaling-group-test\t",
        "MultiAZPolicy": "PRIORITY",
        "LifecycleState": "Active",
        "ServerGroupAttributes": [
          {
            "LoadBalancerId": "clb-12augb3oetgxs17q7y24a****\t",
            "ServerGroupId": "rsp-12b2z5fnxvhts17q7y2fj****\t",
            "Port": 80,
            "Weight": 20,
            "Type": "CLB"
          },
        ],
        "DBInstanceIds": [
          "rds-mysql-42b38c76****"
        ],
        "SubnetIds": [
          "subnet-24sdlkdplsjkdjd****"
        ],
        "VpcId": "vpc-2fevwte3frk0059gp67d6****",
        "UpdatedAt": "2022-04-14T18:29:38+08:00",
        "TotalInstanceCount": 1,
        "MinInstanceNumber": 0,
        "MaxInstanceNumber": 100,
        "CreatedAt": "2022-04-10T18:29:38+08:00",
        "DesireInstanceNumber": 1,
        "LaunchTemplateOverrides": [
          {
            "InstanceType": "ecs.g2a.large",
            "WeightedCapacity": 1,
            "PriceLimit": 0.001
          },
        ],
        "LaunchTemplateId": "lt-yc5kwj1di33uw1qj****",
        "LaunchTemplateVersion": "Default",
        "StoppedInstanceCount": 10,
        "HealthCheckType": "ECS",
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          },
        ],
        "ScalingMode": "release",
        "ProjectName": "default",
        "InstancesDistribution": {
          "OnDemandBaseCapacity": 0,
          "OnDemandPercentageAboveBaseCapacity": 0,
          "CompensateWithOnDemand": true,
          "SpotInstanceRemedy": true
        },
        "LoadBalancerHealthCheckGracePeriod": 60,
        "SuspendedProcesses": [
          "ScaleIn"
        ]
      },
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |LimitExceeded.ScalingGroupIds |You've reached the limit on the number of ScalingGroupIds. |The number of scaling group IDs reaches the upper limit. |
|400 |LimitExceeded.ScalingGroupNames |You've reached the limit on the number of ScalingGroupNames. |The number of scaling group names reaches the upper limit. |
|400 |LimitExceeded.TagFilterKeys |You've reached the limit on the number of TagFilter Keys that you can set. |The upper limit of the number of tag filter keys is reached. |
|400 |MissingParameter.TagKey |The required parameter TagFiltersKey is not supplied. |The tag filter key cannot be empty. |
|400 |LimitExceeded.TagFiltersValues |You've reached the limit on the number of TagFilters.N.Values that you can set. |The upper limit of the number of tag filter values is reached. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |A conflict with the specified tag filter key occurs. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
