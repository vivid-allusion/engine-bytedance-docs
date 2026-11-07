---
title: "ModifyInstanceChargeType - Changes the billing methods of instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType"
---

Call the ModifyInstanceChargeType operation to switch billing methods between pay\-as\-you\-go and subscription for instances.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* When you change the billing method of an instance from pay\-as\-you\-go to subscription, the billing method of the system volume is automatically changed synchronously. You can choose whether to change the billing methods of the currently mounted data volumes from pay\-as\-you\-go to subscription. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription)

* When you change the billing method of an instance from subscription to pay\-as\-you\-go, the billing methods of the system volume and data volumes mounted to the instance are synchronously changed to pay\-as\-you\-go. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go)

* This operation does not apply to EIPs associated with the instance.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceChargeType&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|H4hGpt">必选</span> `Sample value: ModifyInstanceChargeType`

The operation that you want to perform. Valid value: ModifyInstanceChargeType.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|kfnC5b">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**AutoPay ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to enable automatic payment. Valid values:


* true: Enables automatic payment. You need to make sure that the account balance is sufficient. If the account balance is insufficient, an abnormal order will be generated and the billing method change will fail.

* false (default): Only an order is generated but no fee is deducted. You can log in to the BytePlus order management page to complete payment after the order is generated.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your account balance is insufficient, we recommend that you set this parameter to <code>false</code>.</div>




**AutoRenew ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to automatically renew the instance after it expires. Value:


* true: Enables automatic renewal

* false (default): Disables automatic renewal


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**AutoRenewPeriod ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The renewal length for each automatic renewal.


* This parameter is valid only when the value of the `AutoRenew` parameter is `true`. The default value is 1.

* When the value of `PeriodUnit` is `Month`, the value of `AutoRenewPeriod` can be 1, 2, 3, 6, or 12.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client automatically generates a token to ensure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to only precheck this request. Value:


* true: Sends a check request without changing the billing method. Check items include: whether required parameters are filled, request format, business restrictions, and ECS inventory. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

* false (default): Sends a check request and changes the billing method after the check is passed.



**IncludeDataVolumes ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to change the billing methods from pay\-as\-you\-go to subscription for all data volumes mounted to the instance.


* true: Changes the billing methods.

* false (default): Does not change the billing methods.



**InstanceChargeType ** <span data-label="purple">string </span>`Optional` `Sample value: PostPaid`

The target billing method of the instance. Valid values:


* PrePaid (default): Changes the billing method from pay\-as\-you\-go to subscription.

* PostPaid: Changes the billing method from subscription to pay\-as\-you\-go.



**InstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|1xFlJG">必选</span> `Sample value: InstanceIds.1=i-3thhlu8byl4bwbha****`

The instance ID. Up to 20 instance IDs are supported.


* Parameter \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with ampersands (&).



**Period ** <span data-label="purple">integer </span>`Optional` `Sample value: 2`

The purchase duration of resources. Valid values:

1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>InstanceChargeType</code> is set to <code>PrePaid</code>, this parameter takes effect and is required.</div>




**PeriodUnit ** <span data-label="purple">string </span>`Optional` `Sample value: Month`

The unit of purchase duration of resources, which is the unit of the `Period` parameter. Valid values:


* Month (default)

* Week (not yet supported)



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderId ** <span data-label="purple">string </span>`Sample value: Order7021038849342******`

The order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstanceChargeType&Version=2020-04-01&InstanceIds.1=i-4ay51iinvo8w4nho****&InstanceChargeType=PrePaid&PeriodUnit=Month&Period=2&AutoPay=True&IncludeDataVolumes=false HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyInstanceChargeType",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order7021038849342******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidAffinityGroupInstanceForModifyInstanceChargeType.Unsupported |The specified affinity group instance does not support modify instance charge type. |The specified instance is an affinity group instance, which does not allow you to change its billing method. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostInstanceForModifyInstanceChargeType.Unsupported |The specified instance is on dedicated host, cannot be used to modify instance charge type. |The specified instance is on a dedicated host, which does not support billing method changes. |
|400 |InvalidInstanceChargeType |The specified InstanceChargeType is invalid. |The specified instance billing method is invalid. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidPeriod |The specified period is not valid. |The specified number of billing cycles is invalid. |
|400 |InvalidPeriodUnit |The specified PeriodUnit is not valid, is unsupported, or cannot be used. |The specified billing cycle is invalid. |
|400 |InvalidScheduledInstanceForModifyInstanceChargeType.Unsupported |The specified scheduled instance cannot be used to modify instance charge type. |The specified Elastic Scheduled Instance (ESI) does not support billing method changes. |
|400 |InvalidSpotStrategyForModifyInstanceChargeType.Unsupported |The specified SpotStrategy cannot be used to modify instance charge type. |The spot policy of the specified instance does not support billing method changes. |
|400 |LimitExceeded.MaximumInstanceIds |You've reached the limit on the number of InstanceIds that you can set. |The specified number of instance IDs exceeds the upper limit. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceCpus |You've reached the limit on the number of instance CPU that you can create, please submit ticket to request an increase in quota. |The quota of instance CPU number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceTypeInstances |You've reached the limit on the number of instance type instances that you can create, please submit ticket to request an increase in quota. |The quota of the number of the specified instance type that you can create is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstances |You've reached the limit on the number of instances that you can create, please submit ticket to request an increase in quota. |The quota of the instance number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumLocalVolumeCpus |You've reached the limit on the number of local volume instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu] quota. |The CPU quota of the Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGeneralCpus |You've reached the limit on the number of general reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu_ri_regional] quota. |The CPU quota of the general\-purpose instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic_ri_regional] quota. |The GPU card quota of regional RIs that can be used for purchasing GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance_ri_regional] quota. |The GPU card quota for HPC\-optimized instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus |You've reached the limit on the number of local volume reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu_ri_regional] quota. |The CPU quota of regional RIs that can be used for purchasing Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumVolumes |You've reached the limit on the capacity of Volumes that you can create, please submit ticket to request an increase in quota. |The volume quota is insufficient. Please submit a ticket to request a quota increase. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |InvalidInstance.Expired |The specified instance has expired. |The instance has expired. |
|412 |OperationDenied.AffinityGroupInstance |The specified operation is denied as your instance is an affinity group instance, and all instanceIds the affinity group must be specified. |The specified operation is rejected because the instance is an affinity group instance, and you must specify the IDs of all instances in the affinity group. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The resources are currently insufficient. Try again later or select other instance types. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
