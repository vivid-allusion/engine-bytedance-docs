---
title: "ModifyScalingGroup - Modifies a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/ModifyScalingGroup"
---

Modify basic information and the associated subnet of a scaling group. If optional parameters are not provided, they will not be modified. For operation instructions, refer to [Modifying instance quantity of scaling groups](https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyScalingGroup&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|oGd2lr">必选</span> `Sample value: ModifyScalingGroup`

The action that you want to perform. Value: ModifyScalingGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|G5f3Zr">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**HealthCheckType ** <span data-label="purple">string </span>`Optional` `Sample value: ECS`

Indicates the health check method of the scaling group. Value range:


* NONE (default): No health check for instances.

* ECS: Performs health check for ECS instances in the scaling group.



**MultiAZPolicy ** <span data-label="purple">string </span>`Optional` `Sample value: PRIORITY`

The scaling policy for the scaling group with multi\-subnet configuration. Valid values:


* PRIORITY: Priority policy.

* BALANCE: Balanced distribution policy.


For details on subsequent instance scaling activities, refer to the "Scaling Policy" parameter description in [Creating scaling groups](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group).



**InstancesDistribution.OnDemandBaseCapacity ** <span data-label="purple">integer </span>`Optional` `Sample value: 200`

The minimum number of pay\-as\-you\-go instances in the scaling group. Value range: 0 ~ 2000. When the number of pay\-as\-you\-go instances in the group is less than the specified value, creating pay\-as\-you\-go instances is prioritized.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is effective only when the billing method of the <a href="https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources">scaling configuration source</a> associated with the scaling group is of the spot type. This parameter does not affect the final number of instances created. The number of instances is restricted by the maximum, minimum, and expected number of instances limits.</div>




**LaunchTemplateOverrides.N.InstanceType ** <span data-label="purple">string[] </span>`Optional` `Sample value: ecs.g2a.large`

Specifies the instance type.


* Parameter \- N: Indicates the serial number of the instance type. Valid range: 1–10.

* Parameter \- InstanceType: Indicates the instance type.

* Multiple instance types are separated by &.

* If this parameter is specified, the specified instance type overrides the instance type associated with the launch template.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when a value is specified for the LaunchTemplateId parameter.</div>




**LaunchTemplateVersion ** <span data-label="purple">string </span>`Optional` `Sample value: Default`

The version of the instance launch template. Valid values:


* The version number of a specific version of the template.

* Default: The template's default version is always used.

* Latest: The template's latest version is always used.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is effective only when a value is passed in for the LaunchTemplateId parameter.</div>




**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-yc5kwj1di33uw1qj****`

The ID of the instance launch template. The specified launch template is then used as the scaling configuration source.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|KPfrB0">必选</span> `Sample value: scg-yblhryq64wgh9zmp****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**SubnetIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: subnet-24sdlkdplsjkdjd****`

The ID list of subnets of primary network interfaces of instances in the scaling group. During subnet ID modification, the VPC cannot be changed. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) operation to query the subnet ID and the VPC to which the subnet belongs.

Parameter \- N: Indicates the serial number of the subnet. Multiple subnets can be selected. The selected subnets need to be under the same VPC. Only one subnet can be selected in the same availability zone.



**InstancesDistribution.CompensateWithOnDemand ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to allow using pay\-as\-you\-go instances to supplement spot instance capacity. Specifically, this parameter specifies whether to create pay\-as\-you\-go instances to supplement capacity when spot instances can not be created as expected due to price, stock, or other reasons. Valid values:


* true: Allows.

* false: Does not allow.



**InstancesDistribution.SpotInstanceRemedy ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Indicates whether to allow replacing spot instances which are about to expire. If replacement is allowed, about 5 minutes before reclamation of the current spot instance, a new spot instance will be created in the scaling group to replace it. Valid values:


* true: Allows.

* false: Does not allow.



**InstancesDistribution.OnDemandPercentageAboveBaseCapacity ** <span data-label="purple">integer </span>`Optional` `Sample value: 0`

Specifies the proportion of pay\-as\-you\-go instances after the minimum pay\-as\-you\-go instance count of the scaling group is met. Value range: 0–100. Specifies the proportion of pay\-as\-you\-go instances after the minimum pay\-as\-you\-go instance count of the scaling group is met. Value range: 0–100.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is effective only when the billing method of the <a href="https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources">scaling configuration source</a> associated with the scaling group is of the spot type.</div>




**LaunchTemplateOverrides.N.PriceLimit ** <span data-label="purple">float[] </span>`Optional` `Sample value: 0.001`

Specifies the maximum hourly price of the spot instance.


* Parameter \- N: Specifies the serial number of the instance type. Valid value: 1–10.

* Value \- PriceLimit: The maximum hourly price for the spot instance type. Value: greater than 0, with a maximum of 3 decimal places.

* Use & to separate multiple prices.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the <code>LaunchTemplateId</code> parameter is specified, and the billing mode specified in the launch template is of the spot type with a price upper limit (which is SpotWithPriceLimit).</div>




**ActiveScalingConfigurationId ** <span data-label="purple">string </span>`Optional` `Sample value: scc-yblhz5oxzml8j1gv****`

The ID of the scaling configuration associated with the scaling group. You can call [DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) to query the scaling configuration ID.



**DefaultCooldown ** <span data-label="purple">integer </span>`Optional` `Sample value: 300`

The cooldown interval after an adjustment is executed (adding or removing ECS instances).

During the interval, the scaling group does not perform other scaling activities. This rule applies only to scaling activities based on Cloud Monitor alert tasks triggered by scaling rules.

Value range: 5 ~ 86400. Unit: seconds.



**DesireInstanceNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 2`

The expected number of instances running in the scaling group. For more information, refer to [Expected instance count](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity).


* When the expected number of instances is changed, a health check is triggered immediately, and the number of instances in the group changes accordingly.

* Value: No less than the minimum number of instances (MinInstanceNumber) and no greater than the maximum number of instances (MaxInstanceNumber).



**InstanceTerminatePolicy ** <span data-label="purple">string </span>`Optional` `Sample value: NewestInstance`

The instance removal policy. Valid values:


* OldestInstance: Removes the instance that was added earliest (**automatically created or manually added**) to the scaling group.

* NewestInstance: Removes the instance that was added most recently (**including those automatically created and manually added**) to the scaling group.

* OldestScalingConfigurationWithOldestInstance (default): Removes the earliest instance **automatically created** in the scaling group based on the earliest scaling configuration of the group.

* OldestScalingConfigurationWithNewestInstance: Removes the most recently **created instance automatically** in the scaling group based on the earliest scaling configuration of the group.



**MaxInstanceNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 3`

The maximum number of instances in the scaling group. The default value range is 0 to 100.



**MinInstanceNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The minimum number of instances in the scaling group. The default value range is 0 to 100.



**ScalingGroupName ** <span data-label="purple">string </span>`Optional` `Sample value: scaling-group-test`

Indicates the name of the scaling group. Scaling group names cannot be duplicated in the same region. Valid values:


* It must start with a letter or Chinese character.

* It can contain only Chinese characters, letters, numbers, underscores, and hyphens.

* The name must be 1 to 128 characters in length.

* Special characters are currently not supported.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingGroupId ** <span data-label="purple">string </span>`Sample value: scg-yblhryq64wgh9zmp****`

The ID of the scaling group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyScalingGroup&ScalingGroupId=scg-yblhryq64wp****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T092959Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024050717301203918304911202AAF7",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingGroupId": "scg-yblhryq64wgh9zmp****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidScalingGroup.InvalidStatus |The specified ScalingGroup is not in the correct status. |The current status of the specified scaling group does not support this operation. |
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |InvalidScalingGroupName.Malformed |The specified ScalingGroupName is malformed. |The specified scaling group name is invalid. |
|400 |InvalidDefaultCooldown.Malformed |The specified DefaultCooldown is malformed. |The specified cooldown time is invalid. |
|400 |InvalidHealthCheckType |The specified HealthCheckType is unsupported. |The specified type of health check is not supported. |
|400 |InvalidLoadBalancerHealthCheckGracePeriod.Malformed |The specified LoadBalancerHealthCheckGracePeriod is malformed. |The grace period of Load Balancer is invalid. |
|400 |LimitExceeded.SubnetIds |You've reached the limit on the number of SubnetIds. |The maximum number of subnet IDs is reached. |
|400 |InvalidScalingConfiguration.ScalingGroupMismatch |The specified ScalingConfiguration [%s] does not match ScalingGroup [%s]. |The specified scaling configuration does not match the scaling group. |
|400 |InvalidScalingConfigurationAndLaunchTemplate.Conflict |The specified ScalingConfiguration conflicts with LaunchTemplate. |The scaling configuration and launch template are duplicated. |
|400 |InvalidOnDemandPercentageAboveBaseCapacity.Malformed |The specified OnDemandPercentageAboveBaseCapacity is malformed. |The specified proportion of pay\-as\-you\-go instances beyond capacity is invalid. |
|400 |InvalidOnDemandBaseCapacity.Malformed |The specified OnDemandBaseCapacity is malformed. |The specified minimum number of pay\-as\-you\-go instances is invalid. |
|400 |InvalidMinInstanceNumber.Malformed |The specified MinInstanceNumber is malformed. |The specified minimum number of instances is invalid. |
|400 |InvalidMultiAZPolicy |The specified MultiAZPolicy is unsupported. |The specified multi\-availability zone policy is not supported. |
|400 |InvalidDesireInstanceNumber.Malformed |The specified DesireInstanceNumber is malformed. |The specified expected number of instances is invalid. |
|400 |InvalidInstanceTerminatePolicy |The specified InstanceTerminatePolicy is unsupported. |The specified instance removal policy is not supported. |
|400 |InvalidMaxInstanceNumber.Malformed |The specified MaxInstanceNumber is malformed. |The specified maximum number of instances is invalid. |
|400 |LimitExceeded.LaunchTemplateOverrides |You've reached the limit on the number of LaunchTemplateOverrides. |The maximum number of extended parameters for the launch template is reached. |
|400 |InvalidLaunchTemplateVolumeSize.ImageSizeMismatch |The specified LaunchTemplate VolumeSize is smaller than the ImageSize. |The system volume size of the specified launch template is smaller than that of the image. |
|400 |InvalidLaunchTemplateHostName.Malformed |The specified LaunchTemplate HostName is malformed. |The name of the host machine of the specified launch template is invalid. |
|400 |MissingParameter.LaunchTemplateVolumes |The required parameter LaunchTemplate Volumes is not supplied. |The volume information of the specified launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateInstanceType |The required parameter LaunchTemplate InstanceType is not supplied. |The instance type of the specified launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateImageId |The required parameter LaunchTemplate ImageId is not supplied. |The ID of the image associated with the specified launch template cannot be empty. |
|400 |InvalidLaunchTemplateId.VersionMismatch |The specified LaunchTemplateId [%s] and LaunchTemplateVersion [%s] are mismatched. |The ID and version of the specified launch template do not match. |
|400 |InvalidLaunchTemplateVersion.Malformed |The specified LaunchTemplateVersion is malformed. |The specified version of the launch template is invalid. |
|400 |MissingParameter.LaunchTemplateId |The required LaunchTemplateId is not supplied. |The ID of the launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateVersion |The required LaunchTemplateVersion is not supplied. |The version of the launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateInstanceName |The required parameter LaunchTemplate InstanceName is not supplied. |The instance name of the specified launch template cannot be empty. |
|400 |InvalidMaxInstanceNumber.ScheduledInstanceExceed |The MaxInstanceNumber is malformed due to the ScheduledInstance existing. |The maximum number of instances is invalid due to ESI existence. |
|400 |MissingParameter.SubnetIds |The required parameter SubnetIds is not supplied. |The subnet ID cannot be left empty. |
|400 |InvalidLaunchTemplate.VpcIDMismatch |The specified LaunchTemplate VpcId is different from ScalingGroup VpcId. |The specified launch template and scaling group are not in the same VPC. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidSubnetId.NotFound |The specified SubnetId [%s] does not exist. |The specified subnet ID does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidLaunchTemplateImageId.NotFound |The specified LaunchTemplate ImageId does not exist. |The ID of the image associated with the specified launch template does not exist. |
|404 |InvalidScalingConfiguration.NotFound |The specified ScalingConfiguration [%s] does not exist. |The specified scaling configuration does not exist. |
|409 |InvalidScalingGroupName.Conflict |The specified ScalingGroupName already existed. |The specified scaling group name already exists. |
|409 |InvalidSubnetId.Conflict |The specified SubnetId [%s] already existed. |The specified subnet ID already exists. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
