---
title: "PurchaseReservedInstances - Purchases Reserved Instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances"
---

Call the PurchaseReservedInstances operation to purchase [offsetting resources](https://docs.byteplus.com/en/docs/ecs/Overview-of-deductible-resources) (RI or RSC).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=PurchaseReservedInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|kTuqym">必选</span> `Sample value: PurchaseReservedInstances`

The action that you want to perform. Value: PurchaseReservedInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|65DJ95">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**AutoRenew** <span data-label="purple">boolean</span> `Optional` `Sample value: true`

Whether to automatically renew the RI after its expiration.


* true: Enable automatic renewal.

* false (default): Does not enable automatic renewal.



**AutoRenewPeriod** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The renewal length for each automatic renewal.


* When `AutoRenew` is set to `True`, this parameter is valid.

* When `PeriodUnit` is set to `Month`, valid values are​ 1, 2, 3, 6, and 12. Default value is 1.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: testDescription`

RI description. Default value: empty string.


* It must start with a letter or Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.



**EffectiveAt** <span data-label="purple">string</span> `Optional` `Sample value: 2025-03-29T17:00:00+08:00`

The RSC effective time. This parameter defaults to empty string which indicates that RSC takes effect immediately after purchase.

If the specified effective time is not on the hour, RSC takes effect at the current hour of the specified time. For example, if the specified time is 2025\-03\-29T17:50:00+08:00, the actual effective time is 2025\-03\-29T17:00:00+08:00.



**HpcClusterId** <span data-label="purple">string</span> `Optional` `Sample value: hpcCluster-1`

When you purchase RIs for HPC\-optimized instances, specify the HPC cluster ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to purchase RI for this type of instance, contact the account manager to apply.</div>




**InstanceCount** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The number of Pay\-as\-you\-go instances that can be deducted or reserved with RIs. Value: 1–100. When 0 is passed in or no parameter is passed in, the default number is 1.

For example, if you have a zonal RI for the ecs.ecs.g3i.large instance type and set the instance count to 2, this RI can match 2 pay\-as\-you\-go instances of the same type at the same time.



**InstanceTypeId** <span data-label="purple">string</span> <span data-api-tag="require|GHNCai">必选</span> `Sample value: ecs.g3i.large`

Instance type that can be deducted or reserved by RIs.



**Period** <span data-label="purple">integer</span> `Optional` `Sample value: 12`

Subscription duration of RIs (month)


* Values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36

* Default value: 1



**PeriodUnit** <span data-label="purple">string</span> `Optional` `Sample value: Month`

The unit of purchase duration of RI. Value: Month.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The associated project. Each instance can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**RegionId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing`

The ID of the region specified in RI.

You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/ecs/DescribeRegions) operation to view the region ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Scope</code> is set to <code>RegionalRI</code>, this parameter is required.</div>




**ReservedCapacity** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The capacity that can be reserved by RSC per hour, measured in GiB/hour or TiB/hour.

Value range: 65535 GiB to 64 TiB


* The total capacity of the package is calculated as `ReservedCapacity` multiplied by the number of hours in the validity period. Meanwhile, the maximum amount that can be deducted each hour is `ReservedCapacity` \* 2.

* When `ReservedStorageCapacityName` is empty, this parameter is optional and invalid.

* When `ReservedStorageCapacityName` is not empty, this parameter is required.



**ReservedInstanceName** <span data-label="purple">string</span> <span data-api-tag="require|1xUN2y">必选</span> `Sample value: reserved-instance-test`

Enter the RI name.


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Can only contain Chinese characters, letters, digits, underscores "_" and hyphens "\-"

* The length limit is 1 to 128 characters.

* Special characters are currently not supported.



**ReservedStorageCapacityName** <span data-label="purple">string</span> `Optional` `Sample value: RSC01`

Enter the RSC name.


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length limit is 1 to 128 characters.

* Special characters are currently not supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An empty parameter indicates no RSC is purchased.</div>




**RscAutoRenew** <span data-label="purple">boolean</span> `Optional` `Sample value: true`

Whether to automatically renew the RSC after its expiration. Value:


* true: Enable automatic renewal

* false (default): Disable automatic renewal



**RscAutoRenewPeriod** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The renewal length for each automatic renewal of RSC.


* When `RscAutoRenew` is set to `True`, this parameter is valid.

* When `PeriodUnit` is set to `Month`, this parameter takes one of the values 1, 2, 3, 6, or 12. The default value is 1.



**Scope** <span data-label="purple">string</span> `Optional` `Sample value: ZonalRI`

RI type. Value:


* ZonalRI (default): zonal RI

* RegionalRI: regional RI. Regional RI is currently in Beta. If you need a trial, contact the account manager to apply.



**Tags.N.Key** <span data-label="purple">string[]</span> <span data-api-tag="require|85u52t">必选</span> `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the user tag.


* Parameter \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any combination of uppercase and lowercase letters.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The value of the user tag.


* Parameter \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in Tags.N.Key first.</div>




**VolumeType** <span data-label="purple">string</span> `Optional` `Sample value: ESSD_PL0`

The volume type. Valid values:


* ESSD_PL0: ESSD PL0

* ESSD_FlexPL: ESSD FlexPL


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>ReservedStorageCapacityName</code> is empty, this parameter is optional and invalid.</div>


* <div data-tips="true" data-tips-type="tip">When <code>ReservedStorageCapacityName</code> is not empty, this parameter is required.</div>




**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone specified in RI.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Scope</code> is set to <code>ZonalRI</code>, this parameter is required.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ReservedInstanceId** <span data-label="purple">string</span> `Sample value: ecsri-ycq8kgnlxrb5oxt0****`

ID of RI.



**ReservedStorageCapacityId** <span data-label="purple">string</span> `Sample value: ebsrsc-3tigy72q3u3vj0x2****`

RSC ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=PurchaseReservedInstances&Version=2020-04-01&RegionId=cn-beijing&ZoneId=cn-beijing-a&ReservedInstanceName=reserved-instance-test&InstanceTypeId=ecs.g3i.large HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "PurchaseReservedInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "ReservedInstanceId": "ecsri-ycq8kgnlxrb5oxt0****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidConfiguration.Unsupported |The specified configuration includes an unsupported operation. |The selected configuration is temporarily not available for sale. |
|400 |InvalidCount.Malformed |The specified count is malformed. |The specified parameter Count is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |InvalidInstanceTypeForCreateReservedInstance.Unsupported |The specified InstanceType does not support creation of reserved instances. |The specified instance type does not support RIs. |
|400 |InvalidPeriod |The specified period is not valid. |The specified number of billing cycles is invalid. |
|400 |InvalidPeriodUnit |The specified PeriodUnit is not valid, is unsupported, or cannot be used. |The specified billing cycle is invalid. |
|400 |InvalidReservedInstanceName.Malformed |The specified ReservedInstanceName is malformed. |The specified ReservedInstanceName is invalid. |
|400 |InvalidReservedStorageCapacityName.Malformed |The specified ReservedStorageCapacityName is malformed. |The specified ReservedStorageCapacityName is invalid. |
|400 |InvalidScope.Malformed |The specified Scope is malformed. |The specified level in RI is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidVolumeType.Malformed |The specified VolumeType is malformed. |The specified volume type is invalid. |
|400 |LimitExceeded.MaximumInstanceCount |The number of specified InstanceCount exceeds the maximum limit. |The specified InstanceCount exceeds the upper limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |LimitExceeded.MinimumInstanceCount |The number of specified InstanceCount exceeds the minimum limit. |The specified InstanceCount exceeds the lower limit. |
|400 |LimitExceeded.ReservedCapacitySize |The specified reserved capacity size exceeds the limit. |The specified RSC (GiB) exceeds the limit. |
|400 |MissingParameter.InstanceTypeId |The required parameter InstanceTypeId is not supplied. |The ID of the instance type can not be empty. |
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
|400 |QuotaExceeded.MaximumReservedInstanceTypeInstances |You've reached the limit on the number of reserved instance type instances that you can create, please submit ticket to request an increase in quota. |The quota of the number of specified instance type that you can create with RI is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstances |You've reached the limit on the number of reserved instances that you can create, please submit ticket to request an increase in quota. |The quota of instance number that can be reserved is insufficient. Please submit a ticket to request a quota increase. |
|404 |InvalidHpcCluster.NotFound |The specified HpcCluster does not exist. |The specified HPC cluster does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidRegion.NotFound |The specified region does not exist. |The specified region does not exist. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |OperationDenied.ReservedStorageCapacityNotAvailable |The specified operation is denied as the reserved storage capacity is not available. |This feature for RSC is not available. Please contact the administrator. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The capacity resources are currently insufficient. Please try again later or select other instance types. |
|500 |Insufficient.VolumePoolCapacity |There is not enough capacity to fulfill your request. |Insufficient capacity of the current storage pool. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
