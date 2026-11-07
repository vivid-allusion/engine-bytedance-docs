---
title: "ModifyReservedInstances - Changes Reserved Instances (RI)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyReservedInstances"
---

Call the ModifyReservedInstances operation to modify Reserved Instances, including changing their attributes and splitting/merging them.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* You can first learn about the limits of this feature by referring to [Changing Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances).

* For ease of description, in this topic, the Reserved Instances to be changed are referred to as the source Reserved Instances, and the changed Reserved Instances obtained are referred to as the target Reserved Instances.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, if you do not pass in optional parameters, the original configuration is retained.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyReservedInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|ctNISS">必选</span> `Sample value: ModifyReservedInstances`

The operation that you want to perform. Valid value: ModifyReservedInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|NIQUVr">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**AutoRenew** <span data-label="purple">boolean</span> `Optional` `Sample value: true`

Whether to automatically renew the target Reserved Instances when they expire. Valid values:


* true: Enable automatic renewal.

* false (default): Does not enable automatic renewal.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you enable automatic renewal, the platform automatically deducts the renewal fees before the expiration of all target Reserved Instances generated this time. You do not need to manually renew them.</div>




**AutoRenewPeriod** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The renewal length for each automatic renewal.


* This parameter takes effect only when the value of the `AutoRenew` parameter is `true`.

* When the value of `PeriodUnit` is `Month`, the value of this parameter can be 1, 2, 3, 6, and 12. Default value: 1.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Configurations.N.ReservedInstanceName** <span data-label="purple">string[]</span> <span data-api-tag="require|bbcHWI">必选</span> `Sample value: Configurations.1.ReservedInstanceName=reserved-instance-test`

The name of the target Reserved Instance.


* Parameter \-N: Specifies the serial number of the Reserved Instance. The value of N ranges from 1 to 50.

* Separate multiple Reserved Instances with &.



**Configurations.N.HpcClusterId** <span data-label="purple">string[]</span> `Optional` `Sample value: Configurations.1.HpcClusterId=hpcCluster-1`

HPC Cluster ID.


* Parameter \-N: Specifies the serial number of the Reserved Instance.

* Separate multiple Reserved Instances with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when the instance type of the Reserved Instance is HPC\-optimized.</div>




**Configurations.N.InstanceCount** <span data-label="purple">integer[]</span> `Optional` `Sample value: Configurations.1.InstanceCount=2`

The number of pay\-as\-you\-go instances that can be offset by the target Reserved Instance. Maximum value: 100. If 0 is passed in or no value is passed, the default value is 1.


* Parameter \-N: Specifies the serial number of the Reserved Instance. The value of N ranges from 1 to 50.

* Separate multiple Reserved Instances with &.



**Configurations.N.InstanceTypeId** <span data-label="purple">string[]</span> `Optional` `Sample value: Configurations.1.InstanceTypeId=ecs.g3i.xlarge`

The IDs of the instance types that can be matched by the target Reserved Instances.


* Parameter \-N: Specifies the serial number of the Reserved Instance. The value of N ranges from 1 to 50.

* Separate multiple Reserved Instances with &.



**Configurations.N.Scope** <span data-label="purple">string[]</span> `Optional` `Sample value: Configurations.1.Scope=ZonalRI`

The type of the target Reserved Instances. Valid values:


* ZonalRI: Zonal Reserved Instances.

* RegionalRI: regional RI. Regional RI is currently in Beta. If you need a trial, contact the account manager to apply.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Parameter \-N: Specifies the serial number of the Reserved Instance. The value of N ranges from 1 to 50.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple Reserved Instances with &.</div>




**Configurations.N.ZoneId** <span data-label="purple">string[]</span> `Optional` `Sample value: Configurations.1.ZoneId=cn-beijing-a`

The ID of the availability zone where the target Reserved Instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.


* Parameter \-N: Specifies the serial number of the Reserved Instance. The value of N ranges from 1 to 50.

* Separate multiple Reserved Instances with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of <code>Configurations.N.Scope</code> is <code>ZonalRI</code>, this parameter is required.</div>




**Description** <span data-label="purple">string</span> `Optional` `Sample value: testDescription`

The description of the Reserved Instance.


* Start with a letter or a Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When an empty string is passed in, the existing description will be cleared.</div>




**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The associated project. Each instance can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**RegionId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing`

The ID of the region where the source Reserved Instance resides.

You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/ecs/DescribeRegions) operation to view the region ID.



**ReservedInstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|1oZ3Xo">必选</span> `Sample value: ReservedInstanceIds.1=ecsri-ycsimi9g465p****&ReservedInstanceIds.2=ecsri-ycsimi2db0l8j0wr****`

The ID of the source Reserved Instance. You can specify up to 10 IDs.


* Parameter \-N: Specifies the serial number of the source Reserved Instance.

* Multiple IDs are divided with ampersands (&).



**Tags.N.Key** <span data-label="purple">string[]</span> <span data-api-tag="require|IZqblC">必选</span> `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any case form.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the user tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to pass in this parameter, pass in the <code>Tags.N.Key</code> parameter first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ReservedInstanceIds** <span data-label="purple">string[]</span> `Valid value: ["ecsri-ycspipybqpl8j084****","ecsri-ecsri-yccazceloyf80n48****"]`

The ID of the Reserved Instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyReservedInstances&Version=2020-04-01&ReservedInstanceIds.1=ecsri-ycsimi9g465p****&ReservedInstanceIds.2=ecsri-ycsimi2db0l8j0wr****&Configurations.1.ReservedInstanceName=reserved-instance-test&Configurations.1.InstanceTypeId=ecs.g3i.xlarge&Configurations.1.InstanceCount=2&Configurations.1.Scope=ZonalRI&Configurations.1.ZoneId=cn-beijing-a HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing-a
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20231120161355D7AA5622C4F5C000****",
        "Action": "ModifyReservedInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "ReservedInstanceIds": [
            "ecsri-ycspipybqpl8j084****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceTypeAndInstanceCount |The specified InstanceType And InstanceCount is invalid. |The specified instance type and instance quantity are invalid. |
|400 |InvalidInstanceTypeForCreateReservedInstance.Unsupported |The specified InstanceType does not support creation of reserved instances. |The specified instance type does not support RIs. |
|400 |InvalidPeriod |The specified period is not valid. |The specified number of billing cycles is invalid. |
|400 |InvalidReservedInstanceIds.ZoneMismatch |The specified ReservedInstanceIds are in different Availability Zones. |The specified Reserved Instances do not belong to the same availability zone. |
|400 |InvalidReservedInstanceModifyStatus.Unsupported |The modify status of the specified reserved instance does not support this request. |The current change status of the Reserved Instance does not support this operation. |
|400 |InvalidReservedInstanceName.Malformed |The specified ReservedInstanceName is malformed. |The specified ReservedInstanceName is invalid. |
|400 |InvalidReservedInstanceStatus |The status of the specified reserved instance does not support this request. |The current status of the Reserved Instance does not support this operation. |
|400 |InvalidScope.Malformed |The specified Scope is malformed. |The specified level in RI is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |LimitExceeded.MaximumConfigurations |The number of specified Configurations exceeds the maximum limit. |The value specified for Configurations exceeds the upper limit. |
|400 |LimitExceeded.MaximumInstanceCount |The number of specified InstanceCount exceeds the maximum limit. |The specified InstanceCount exceeds the upper limit. |
|400 |LimitExceeded.MaximumReservedInstanceIds |The number of specified ReservedInstanceIds exceeds the maximum limit. |The value specified for ReservedInstanceIds exceeds the upper limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |LimitExceeded.MinimumInstanceCount |The number of specified InstanceCount exceeds the minimum limit. |The specified InstanceCount exceeds the lower limit. |
|400 |MissingParameter.Configurations |The required parameter Configurations is not supplied. |The Reserved Instance configuration cannot be empty. |
|400 |MissingParameter.ReservedInstanceIds |The required parameter ReservedInstanceIds is not supplied. |You cannot leave the ReservedInstanceIds parameter empty. |
|400 |MissingParameter.ReservedInstanceName |The required parameter ReservedInstanceName is not supplied. |The parameter ReservedInstanceName cannot be empty. |
|400 |MissingParameter.ZoneId |The required parameter ZoneId is not supplied. |Availability zone ID cannot be empty. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumLocalVolumeCpus |You've reached the limit on the number of local volume instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu] quota. |The CPU quota of the Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceCpus |You've reached the limit on the number of reserved instance CPU that you can create, please submit ticket to request an increase in quota. |The quota of instance CPU number that can be reserved is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGeneralCpus |You've reached the limit on the number of general reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu_ri_regional] quota. |The CPU quota of the general\-purpose instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic_ri_regional] quota. |The GPU card quota of regional RIs that can be used for purchasing GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance_ri_regional] quota. |The GPU card quota for HPC\-optimized instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus |You've reached the limit on the number of local volume reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu_ri_regional] quota. |The CPU quota of regional RIs that can be used for purchasing Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceTypeInstances |You've reached the limit on the number of reserved instance type instances that you can create, please submit ticket to request an increase in quota. |The quota of the number of specified instance types that you can create with RI is insufficient. Please submit a ticket to request a quota increase. |
|404 |InvalidHpcCluster.NotFound |The specified HpcCluster does not exist. |The specified HPC cluster does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidRegion.NotFound |The specified region does not exist. |The specified region does not exist. |
|404 |InvalidReservedInstance.NotFound |The specified reserved instance does not exist. |The specified Reserved Instance does not exist. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
|412 |InvalidReservedInstance.ProjectMismatch |The specified reserved instances are in different project. |The specified Reserved Instances do not belong to the same project. |
|412 |InvalidReservedInstanceModifyStatus.ComputeFactorMismatch |The compute factor of the specified reserved instances does not match. |The computing power factors of Reserved Instances are different before and after the change. |
|412 |InvalidReservedInstanceModifyStatus.ExpiredTimeMismatch |The expired time of the specified reserved instances does not match. |The expiration times of the Reserved Instances are different. |
|412 |InvalidReservedInstanceModifyStatus.InstanceTypeFamilyMismatch |The instancetype family of the specified reserved instances does not match. |The instance type families of the Reserved Instances are different. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The capacity resources are currently insufficient. Please try again later or select other instance types. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
