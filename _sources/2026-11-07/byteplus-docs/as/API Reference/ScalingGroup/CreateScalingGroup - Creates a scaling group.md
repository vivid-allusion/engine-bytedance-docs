---
title: "CreateScalingGroup - Creates a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/CreateScalingGroup"
---

Create a scaling group. By default, a created scaling group has default message notifications for scaling activity success/failure. About [message notifications](https://docs.byteplus.com/en/docs/as/Managing_message_notifications).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When your account first accesses the Auto Scaling service via an API operation, the platform automatically initiates the "Cross\-service access authorization" process. This allows the service to access products such as ECS instances or allows other BytePlus products to access the Auto Scaling service.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateScalingGroup&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|svBAuy">必选</span> `Sample value: CreateScalingGroup`

The action that you want to perform. Value: CreateScalingGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|2kRHGx">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**HealthCheckType ** <span data-label="purple">string </span>`Optional` `Sample value: ECS`

Indicates the health check method of the scaling group. Valid values:


* NONE: No health check for instances.

* ECS (default): Performs health check for ECS instances in the scaling group.



**ScalingMode ** <span data-label="purple">string </span>`Optional` `Sample value: release`

The instance reclaim mode of the scaling group. Valid values:


* release (default): Release mode.

* recycle: Stop\-and\-reclaim mode.



**InstancesDistribution.OnDemandBaseCapacity ** <span data-label="purple">integer </span>`Optional` `Sample value: 200`

The minimum number of pay\-as\-you\-go instances in the scaling group. Value range: 0 ~ 2000. When the number of pay\-as\-you\-go instances in the group is less than the specified value, creating pay\-as\-you\-go instances is prioritized.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is effective only when the billing method of the <a href="https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources">scaling configuration source</a> associated with the scaling group is of the spot type. This parameter does not affect the final number of instances created. The number of instances is restricted by the maximum, minimum, and expected number of instances limits.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional Sample value: v1`

The user tag value.


* Parameter \- N: Specifies the serial number of the tag value. Value range: 1–50.

* Separate multiple tag values with &.


Naming rules:


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It can be empty. Length limit: 0–256 characters.

> To pass in this parameter, pass in `Tags.N.Key` first.



**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: k1`

The key of the tag.


* Parameter \- N: Specifies the serial number of the tag key. Value range: 1–50.

* Separate multiple tag keys with &.


Naming rules:


* It cannot start with `volc:` or `sys:` in any combination of uppercase and lowercase letters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Tags that start with <code>volc:</code> or <code>sys:</code> are reserved for the system. You cannot create tags starting with them.   </div>
   

* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.

> Keys of the same resource must be unique.



**LaunchTemplateOverrides.N.InstanceType ** <span data-label="purple">string[] </span>`Optional` `Sample value: ecs.g2a.large`

Specifies the instance type.


* Parameter \- N: Indicates the serial number of the instance type. Valid range: 1–10.

* Parameter \- InstanceType: Indicates the instance type.

* Multiple instance types are separated by &.

* If this parameter is specified, the specified instance type overrides the instance type associated with the launch template. If this parameter is not passed in, the instance type associated with the selected launch template is used.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when a value is specified for the LaunchTemplateId parameter.</div>




**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-yc5kwj1di33uw1qj****`

The ID of the instance launch template. The specified launch template is then used as the scaling configuration source.



**DBInstanceIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: mysql-42b38c769c4b`

The ID of the RDS instance.


* Parameter \- N: Indicates the serial number of the database instance. Valid range: 1–40.

* Separate multiple database instance IDs with &.

* If this parameter is not passed in, this indicates not associating a database instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Associating RDS database instances with scaling groups is in Beta. If you need a trial, please contact your account manager to apply.</div>




**SubnetIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|c5lD2D">必选</span> `Sample value: subnet-24sdlkdplsjkdjd****`

The ID list of subnets of primary network interfaces of instances in the scaling group. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) operation to query subnet IDs.

Parameter \- N: Indicates the serial number of the subnet. Multiple subnets can be selected. The selected subnets need to be under the same VPC. You can select multiple subnets within the same availability zone.



**InstancesDistribution.OnDemandPercentageAboveBaseCapacity ** <span data-label="purple">integer </span>`Optional` `Sample value: 0` 

Specifies the proportion of pay\-as\-you\-go instances after the minimum pay\-as\-you\-go instance count of the scaling group is met. Value range: 0–100.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is effective only when the billing method of the <a href="https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources">scaling configuration source</a> associated with the scaling group is of the spot type.</div>




**LaunchTemplateOverrides.N.PriceLimit ** <span data-label="purple">float[] </span>`Optional` `Sample value: 0.001`

Specifies the maximum hourly price of the spot instance.


* Parameter \- N: Specifies the serial number of the instance type. Valid value: 1–10.

* Value \- PriceLimit: The maximum hourly price for the spot instance type. Value: greater than 0, with a maximum of 3 decimal places.

* Use & to separate multiple prices.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the <code>LaunchTemplateId</code> parameter is specified, and the billing mode specified in the launch template is of the spot type with a price upper limit (which is SpotWithPriceLimit).</div>




**InstancesDistribution.CompensateWithOnDemand ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Indicates whether to create pay\-as\-you\-go instances to supplement capacity when spot instances can not be created as expected due to price, stock, or other reasons. Valid values:


* true: Allows.

* false (default): Does not allow.



**InstancesDistribution.SpotInstanceRemedy ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Indicates whether to allow replacing spot instances which are about to expire. If replacement is allowed, about 5 minutes before reclamation of the current spot instance, a new spot instance will be created in the scaling group to replace it. Valid values:


* true: Allows.

* false (default): Does not allow.



**ServerGroupAttributes.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: CLB`

The type of Load Balancer server groups:


* Parameter \- N: Indicates the serial number of the Load Balancer server group. Value range: 1 ~ 100. One CLB/ALB supports associating up to 20 backend server groups, and all CLBs/ALBs support associating up to 100 backend server groups.

* Parameter \- Type: Indicates the type of the Load Balancer server group.

   * ALB: Application Load Balancer.

   * CLB: Classic Load Balancer.

* Separate multiple server group IDs with ampersands (&).

* If this parameter is not passed in, this indicates not associating with Load Balancer now.

* If this parameter is passed in but no value is specified, CLB is selected by default.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project associated with the scaling group. The default project is automatically used. A resource can belong to only one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs. Values:

Not more than 64 ASCII characters.



**LaunchTemplateVersion ** <span data-label="purple">string </span>`Optional` `Sample value: Default`

The version of the instance launch template. Valid values:


* The version number of a specific version of the template.

* Default (default): The template's default version is always used.

* Latest: Always uses the template latest version.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is effective only when a value is passed in for the LaunchTemplateId parameter.</div>




**ServerGroupAttributes.N.ServerGroupId ** <span data-label="purple">string[] </span>`Optional` `Sample value: rsp-12b2z5fnxvhts17q7y2fj****`

The ID of the Load Balancer backend server group. You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) operation to query the backend server group ID.


* Parameter \- N: Indicates the serial number of the backend server group. Value range: 1 ~ 100.

* Parameter \- ServerGroupId: The server group ID.

* Separate multiple server group IDs with ampersands (&).

* If this parameter is not passed in, this indicates not associating with Load Balancer now.



**DefaultCooldown ** <span data-label="purple">integer </span>`Optional` `Sample value: 300`

The cooldown interval after an adjustment is executed (adding or removing ECS instances). During the interval, the scaling group does not perform other scaling activities. This rule applies only to scaling activities based on Cloud Monitor alert tasks triggered by scaling rules.

Value range: 5 ~ 86400. Unit: seconds. Default value: 300.



**DesireInstanceNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: -1`

The expected number of instances running in the scaling group. For more information, refer to [Expected instance count](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity). Valid values:


* No less than the minimum number of instances (MinInstanceNumber) and no greater than the maximum number of instances (MaxInstanceNumber).

* Default value: \-1, which indicates the expected number of instances feature is not enabled. Immediately after the scaling group is created, a scaling activity will be triggered automatically to add the specified number of instances.



**InstanceTerminatePolicy ** <span data-label="purple">string </span>`Optional` `Sample value: OldestScalingConfigurationWithOldestInstance`

The instance removal policy. Valid values:


* OldestInstance: Removes the instance that was added earliest (**automatically created or manually added**) to the scaling group.

* NewestInstance: Removes the instance that was added most recently (**including those automatically created and manually added**) to the scaling group.

* OldestScalingConfigurationWithOldestInstance (default): Removes the earliest instance **automatically created** in the scaling group based on the earliest scaling configuration of the group.

* OldestScalingConfigurationWithNewestInstance: Removes the most recently **created** instance in the scaling group based on the earliest scaling configuration of the group.



**MaxInstanceNumber ** <span data-label="purple">integer </span><span data-api-tag="require|CTcm3o">必选</span> `Sample value: 10`

The maximum number of instances in the scaling group. The default value range is 0 to 100.



**MinInstanceNumber ** <span data-label="purple">integer </span><span data-api-tag="require|mb2wiM">必选</span> `Sample value: 0`

The minimum number of instances in the scaling group. The default value range is 0 to 100.



**MultiAZPolicy ** <span data-label="purple">string </span>`Optional` `Sample value: PRIORITY`

The scaling policy. If you select multiple subnets, this parameter is required. Valid values:


* PRIORITY (default): Priority policy.

* BALANCE: Balanced distribution policy.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on subsequent instance scaling activities, refer to the "Scaling Policy" parameter description in <a href="https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group">Creating scaling groups</a>.</div>




**ScalingGroupName ** <span data-label="purple">string </span><span data-api-tag="require|mwQf0G">必选</span> `Sample value: scaling-group-test`

Indicates the name of the scaling group. Scaling group names cannot be duplicated in the same region. Valid values:


* Start with a letter or Chinese character only.

* Only Chinese characters, letters, numbers, underscores, and hyphens are allowed.

* The name must be 1 to 128 characters in length.

* Special characters are currently not supported.



**ServerGroupAttributes.N.Port ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 80`

The port number of servers in the Load Balancer backend server group.


* Parameter \- N: Indicates the serial number of the server group. Value range: 1 ~ 20.

* Parameter \- Port: Indicates the port number. Value range: 1 to 65535.

* Separate port numbers of multiple server groups with ampersands (&).

* If this parameter is not passed in, this indicates not associating with Load Balancer now.



**ServerGroupAttributes.N.Weight ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 20`

The weight of the server in the Load Balancer backend server group.


* Parameter \- N: Indicates the serial number of the backend server group. Value range: 1 ~ 5.

* Parameter \- Weight: Indicates the weight. Value range: 0 ~ 100.

* Separate multiple backend server group weights with &.

* If this parameter is not passed in, this indicates not associating with Load Balancer now.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingGroupId ** <span data-label="purple">string </span>`String example: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateScalingGroup&MaxInstanceNumber=10&MinInstanceNumber=0&ScalingGroupName=scaling-group-test&SubnetIds.1=subnet-24sdlkdplsjkdjd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T092442Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507172628156000045004B36439",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request.Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidMultiAZPolicy |The specified MultiAZPolicy is unsupported. |The specified multi\-availability zone policy is not supported. |
|400 |MissingParameter.MinInstanceNumber |The required parameter MinInstanceNumber is not supplied. |The minimum number of instances cannot be empty. |
|400 |MissingParameter.MaxInstanceNumber |The required parameter MaxInstanceNumber is not supplied. |The maximum number of instances cannot be empty. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of Tags that you can create. |The upper limit of tags that you can create is reached. |
|400 |MissingParameter.ScalingGroupName |The required parameter ScalingGroupName is not supplied. |The scaling group name cannot be empty. |
|400 |InvalidSubnet.VPCMismatch |The specified Subnets are in different VPC. |The specified subnet ID is not within the same VPC. |
|400 |InvalidOnDemandBaseCapacity.Malformed |The specified OnDemandBaseCapacity is malformed. |The specified minimum number of pay\-as\-you\-go instances is invalid. |
|400 |InvalidHealthCheckType |The specified HealthCheckType is unsupported. |The specified type of health check is not supported. |
|400 |InvalidScalingGroupName.Malformed |The specified ScalingGroupName is malformed. |The specified scaling group name is invalid. |
|400 |InvalidDefaultCooldown.Malformed |The specified DefaultCooldown is malformed. |The specified cooldown time is invalid. |
|400 |InvalidScalingMode |The specified ScalingMode is unsupported. |The specified instance reclaim mode of the scaling group is not supported. |
|400 |LimitExceeded.ServerGroups |You've reached the limit on the number of ServerGroups that you can attach. |The maximum number of backend server groups that can be associated is reached. |
|400 |InvalidServerGroupWeight.Malformed |The specified ServerGroup Weight is malformed. |The specified backend server weight is invalid. |
|400 |LimitExceeded.LoadBalancerServerGroups |You've reached the limit on the number of [%s] LoadBalancer ServerGroups, max [%d]. |The maximum number of Load Balancer backend servers is reached. |
|400 |InvalidServerGroupPort.Malformed |The specified ServerGroup Port is malformed. |The port of the specified server group is invalid. |
|400 |LimitExceeded.LoadBalancers |You've reached the limit on the number of LoadBalancer, max [%d]. |The maximum number of Load Balancer instances is reached. |
|400 |InvalidOnDemandPercentageAboveBaseCapacity.Malformed |The specified OnDemandPercentageAboveBaseCapacity is malformed. |The specified proportion of pay\-as\-you\-go instances beyond capacity is invalid. |
|400 |LimitExceeded.SubnetIds |You've reached the limit on the number of SubnetIds. |The maximum number of subnet IDs is reached. |
|400 |MissingParameter.ServerGroupId |The required parameter ServerGroupId is not supplied. |The backend server group ID cannot be empty. |
|400 |LimitExceeded.DBInstanceIds |You've reached the limit on the number of DBInstanceIds that you can attach. |The upper limit on the number of associable RDS databases is reached. |
|400 |InvalidInstanceTerminatePolicy |The specified InstanceTerminatePolicy is unsupported. |The specified instance removal policy is not supported. |
|400 |InvalidDesireInstanceNumber.Malformed |The specified DesireInstanceNumber is malformed. |The specified expected number of instances is invalid. |
|400 |InvalidMaxInstanceNumber.Malformed |The specified MaxInstanceNumber is malformed. |The specified maximum number of instances is invalid. |
|400 |InvalidMinInstanceNumber.Malformed |The specified MinInstanceNumber is malformed. |The specified minimum number of instances is invalid. |
|400 |MissingParameter.DBInstanceId |The required parameter DBInstanceId is empty. |RDS instance ID cannot be empty. |
|400 |InvalidDBInstanceId.InvalidStatus |The specified DBInstance [%s] is not in the correct status. |The status of the specified RDS instance is not supported. |
|400 |InvalidDBInstanceID.InvalidVersion |The specified DBInstance [%s] is not in the correct WhiteList Version. |The specified RDS instance version is not supported. |
|400 |InvalidLaunchTemplateId.VersionMismatch |The specified LaunchTemplateId [%s] and LaunchTemplateVersion [%s] are mismatched. |The ID and version of the specified launch template do not match. |
|400 |InvalidLaunchTemplateVersion.Malformed |The specified LaunchTemplateVersion is malformed. |The specified version of the launch template is invalid. |
|400 |MissingParameter.LaunchTemplateId |The required LaunchTemplateId is not supplied. |The ID of the launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateVersion |The required LaunchTemplateVersion is not supplied. |The version of the launch template cannot be empty. |
|400 |QuotaExceeded.Quota |You've reached the limit on the [%s] Quota. |The quota has been reached. |
|400 |InvalidLaunchTemplate.VpcIDMismatch |The specified LaunchTemplate VpcId is different from ScalingGroup VpcId. |The specified launch template and scaling group are not in the same VPC. |
|400 |InvalidLaunchTemplateUserData.Malformed |The specified LaunchTemplate UserData is malformed. |The specified UserData of the launch template is invalid. |
|400 |LimitExceeded.LaunchTemplateUserData |You've reached the limit on the size of LaunchTemplate UserData. |The length of the specified UserData of the launch template reaches the upper limit. |
|400 |InvalidLaunchTemplateInstanceDescription.Malformed |The specified LaunchTemplate InstanceDescription is malformed. |The instance description of the specified launch template is invalid. |
|400 |LimitExceeded.LaunchTemplateInstanceDescription |You've reached the limit on the length of LaunchTemplate InstanceDescription, max [%d] chars. |The instance description length of the specified launch template reaches the upper limit. |
|400 |MissingParameter.LaunchTemplateInstanceName |The required parameter LaunchTemplate InstanceName is not supplied. |The instance name of the specified launch template cannot be empty. |
|400 |InvalidLaunchTemplateInstanceName.Malformed |The specified LaunchTemplate InstanceName is malformed. |The instance name of the specified launch template is invalid. |
|400 |InvalidLaunchTemplateSecurityEnhancementStrategy |The specified LaunchTemplate SecurityEnhancementStrategy is unsupported. |The security enhancement policy of the specified launch template is invalid. |
|400 |MissingParameter.LaunchTemplatePasswordAndKeyPair |The parameters LaunchTemplate Password and KeyPair are both empty. |The password and key pair of the specified launch template cannot both be empty. |
|400 |InvalidLaunchTemplateTagValue.Malformed |The specified LaunchTemplate TagValue is malformed. |The tag value of the specified launch template is invalid. |
|400 |InvalidLaunchTemplateTagKey.Malformed |The specified LaunchTemplate TagKey is malformed. |The tag key of the specified launch template is invalid. |
|400 |LimitExceeded.LaunchTemplateTags |You've reached the limit on the number of LaunchTemplate Tags. |The number of tags of the specified launch template reaches the upper limit. |
|400 |InvalidLaunchTemplateInstanceChargeType |The specified LaunchTemplate InstanceChargeType is unsupported. |The instance billing method of the specified launch template is invalid. |
|400 |MissingParameter.LaunchTemplateEipSecurityProtectionInstanceId |The required parameter LaunchTemplate EIP SecurityProtectionInstanceId is not supplied. |The ID of the EIP security package of the specified launch template cannot be empty. |
|400 |InvalidLaunchTemplateEipBandwidthPackage.Mismatch |The specified eip configuration of LaunchTemplate does not match the bandwidth package [%s] |The EIP and bandwidth package of the specified launch template do not match. |
|400 |InvalidLaunchTemplateEipSecurityProtectionType |The specified LaunchTemplate Eip SecurityProtectionType is unsupported. |The type of EIP security protection of the specified launch template is invalid. |
|400 |InvalidLaunchTemplateEipBillingType |The specified LaunchTemplate Eip BillingType is unsupported. |The billing method of the EIP of the specified launch template is invalid. |
|400 |InvalidLaunchTemplateEipISP |The specified LaunchTemplate Eip ISP is unsupported. |The ISP of the EIP of the specified launch template is not supported. |
|400 |InvalidLaunchTemplateEipBandwidth.Malformed |The specified LaunchTemplate Eip Bandwidth is malformed, range [%d, %d]. |The bandwidth of the EIP associated with the specified launch template is invalid. |
|400 |InvalidLaunchTemplateEipSecurityProtectionInstanceId.Malformed |The specified LaunchTemplate EIP SecurityProtectionInstanceId [%d] is Malformed. |The ID of the EIP security package of the specified launch template is invalid. |
|400 |MissingParameter.LaunchTemplateSecurityGroup |The required parameter LaunchTemplate SecurityGroup is not supplied. |Security group information in the launch template cannot be empty. |
|400 |LimitExceeded.LaunchTemplateSecurityGroups |You've reached the limit on the number of LaunchTemplate SecurityGroups. |The upper limit on the number of security groups associated with the launch template is reached. |
|400 |InvalidLaunchTemplateSpotStrategy |The specified LaunchTemplate SpotStrategy is unsupported. |The spot policy of the specified launch template is invalid. |
|400 |MissingParameter.LaunchTemplateImageId |The required parameter LaunchTemplate ImageId is not supplied. |The ID of the image associated with the specified launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateInstanceType |The required parameter LaunchTemplate InstanceType is not supplied. |The instance type of the specified launch template cannot be empty. |
|400 |InvalidResources.VPCMismatch |The specified ServerGroups And Subnets are in different VPC. |The specified server group and subnet are not in the same VPC. |
|400 |InvalidServerGroup.VPCMismatch |The specified ServerGroups are in different VPC. |The specified backend server group is in a different VPC. |
|400 |LimitExceeded.LaunchTemplateOverrides |You've reached the limit on the number of LaunchTemplateOverrides. |The number of overrides configured in the launch template exceeds the upper limit. |
|400 |InvalidLaunchTemplateVolumeTypes.Mismatch |The specified LaunchTemplate VolumeTypes are mismatched. |The volume type of the specified launch template is invalid. |
|400 |InvalidLaunchTemplateVolumeSize.ImageSizeMismatch |The specified LaunchTemplate VolumeSize is smaller than the ImageSize. |The volume size of the specified launch template is smaller than that of the image. |
|400 |InvalidLaunchTemplateHostName.Malformed |The specified LaunchTemplate HostName is malformed. |The name of the host machine of the specified launch template is invalid. |
|400 |MissingParameter.LaunchTemplateVolumes |The required parameter LaunchTemplate Volumes is not supplied. |The volume information of the specified launch template cannot be empty. |
|400 |MissingParameter.SubnetIds |The required parameter SubnetIds is not supplied. |The subnet ID cannot be left empty. |
|400 |InvalidLoadBalancerHealthCheckGracePeriod.Malformed |The specified LoadBalancerHealthCheckGracePeriod is malformed. |The grace period of Load Balancer is invalid. |
|400 |InvalidServerGroupAttributeType |The required parameter ServerGroupAttributeType is invalid. |The specified server group type is invalid. |
|400 |InvalidVolumeTypeForExtraPerformance.Unsupported |The specified VolumeType does not support extra performance. |The specified volume type does not support additional performance. |
|400 |LimitExceeded.MaximumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the maximum limit. |The specified additional performance throughput (MB) exceeds the maximum limit. |
|404 |InvalidSubnetId.NotFound |The specified SubnetId [%s] does not exist. |The specified subnet ID does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup [%s] does not exist. |The specified backend server group does not exist. |
|404 |InvalidAlbServerGroups |The required parameter ALB ServerGroups is not supplied. |The ALB backend server group cannot be empty. |
|404 |InvalidAlbServerGroups.NotFound |The specified ALB ServerGroups does not exist. |The specified ALB backend server group does not exist. |
|404 |InvalidServerGroupId.NotFound |The specified ServerGroupId [%s] does not exist in LoadBalancer. |The specified server group ID does not exist. |
|404 |InvalidDBInstanceId.NotFound |The specified DBInstanceId [%s] does not exist. |The specified RDS instance ID does not exist. |
|404 |InvalidLaunchTemplateProject.NotFound |The specified Project of LaunchTemplate does not exist. |The project specified in the launch template does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidLaunchTemplateKeyPair.NotFound |The specified LaunchTemplate KeyPair does not exist. |The key pair of the specified launch template does not exist. |
|404 |InvalidLaunchTemplateEipBandwidthPackageId.NotFound |The specified LaunchTemplate Eip BandwidthPackageId [%s] does not exist. |The ID of the EIP shared bandwidth package of the specified launch template does not exist. |
|404 |InvalidLaunchTemplateSecurityGroupId.NotFound |The specified LaunchTemplate SecurityGroupId [%s] does not exist. |The ID of the security group associated with the specified launch template does not exist. |
|404 |InvalidLaunchTemplateImageId.NotFound |The specified LaunchTemplate ImageId does not exist. |The ID of the image associated with the specified launch template does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|409 |InvalidServerGroupId.Conflict |The specified ServerGroupId [%s] Port [%d] already existed. |A port conflict exists for the specified backend server group. |
|409 |InvalidDBInstanceId.Conflict |The specified DBInstanceId [%s] already exists. |Duplicate RDS instance IDs are passed in. |
|409 |InvalidSubnetId.Conflict |The specified SubnetId [%s] already existed. |The specified subnet ID exists. |
|409 |InvalidScalingGroupName.Conflict |The specified ScalingGroupName already existed. |The specified scaling group name already exists. |
|409 |InvalidLaunchTemplateTagKey.Conflict |The specified LaunchTemplate TagKey already existed. |The tag key of the specified launch template is already used. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
