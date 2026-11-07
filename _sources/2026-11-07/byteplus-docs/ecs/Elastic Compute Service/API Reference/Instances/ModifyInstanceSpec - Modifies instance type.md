---
title: "ModifyInstanceSpec - Modifies instance type"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec"
---

Call ModifyInstanceSpec to modify the instance type.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* If the current instance type fails to meet your application requirements or exceeds them, you can first check the available instance type change options for your instance by referring to [Instance types supporting type change](https://docs.byteplus.com/en/docs/ecs/Overview-2). Then, modify the instance type (including vCPU and memory). Both upgrades and downgrades are supported.

* For precautions and usage limits related to changing the instance type, see [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceSpec&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|GPGTon">必选</span> `Sample value: ModifyInstanceSpec`

The operation that you want to perform. Valid value: ModifyInstanceSpec.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|JzatXG">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to only precheck this request. Value:


* true: Sends a check request without changing the instance type. Check items include whether required parameters are filled, request format, business restrictions, and ECS inventory. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

* false (default): Sends a check request and changes the instance type after the check is passed.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|y7vg62">必选</span> `Sample value: i-3thhlu8byl4bwbha****`

The instance ID.



**InstanceTypeId ** <span data-label="purple">string </span><span data-api-tag="require|UW2A6n">必选</span> `Sample value: ecs.g2i.large`

The new instance type.

For information about the instance type families that support instance type change, see [Modifying instance type](https://docs.byteplus.com/en/docs/ecs/Overview-2).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybo349sxoncm9t******`

The ID of the instance on which the operation is performed.



**OrderId ** <span data-label="purple">string </span>`Sample value: Order7021038849342******`

The order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstanceSpec&Version=2020-04-01&InstanceId=i-3thhlu8byl4bwbha****&InstanceTypeId=ecs.g2i.large HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106231950360102251451520133****",
        "Action": "ModifyInstanceSpec",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "i-ybo349sxoncm9t******",
        "OrderId": "Order7021038849342******"
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidAffinityGroupInstanceForModifyInstanceSpec.Unsupported |The specified affinity group instance does not support modify instance specification. |The specified instance is an affinity group instance, which does not support instance type changes. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidInstanceForResizeTypeFamily.Unsupported |The specified instance does not support changing instance specifications across specification families. |The specified instance does not support instance type changes across instance type families. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceType |The specified InstanceType is invalid. |The specified instance type is invalid. |
|400 |InvalidScheduledInstanceForModifyInstanceSpec.Unsupported |The specified scheduled instance cannot be used to modify instance specification. |The specified Elastic Scheduled Instance (ESI) does not support instance type changes. |
|400 |InvalidSpotStrategyForModifyInstanceSpec.Unsupported |The specified SpotStrategy cannot be used to modify instance specification. |The spot policy of the specified instance does not support instance type changes. |
|400 |LimitExceeded.MaximumHighPerformanceNetworkInterfaces |You've reached the limit on the number of HighPerformance NetworkInterfaces that can be attached to the instance. |The number of network interfaces in RDMA communication mode associated with the specified instance exceeds the upper limit. |
|400 |LimitExceeded.MaximumInstancePrivateIpsPerNetworkInterface |The number of specified PrivateIpsPerNetworkInterface exceeds the upper limit of the instance specification. |The number of secondary private IP addresses of the specified network interface exceeds the upper limit of the instance type. |
|400 |LimitExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of NetworkInterfaces that can be attached to the instance. |The specified number of network interfaces associated with the instance exceeds the upper limit. |
|400 |LimitExceeded.MaximumVolumes |You've reached the limit on the number of volumes that can be attached to the instance. |The specified number of volumes mounted to the instance exceeds the upper limit. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|400 |MissingParameter.InstanceTypeId |The required parameter InstanceTypeId is not supplied. |The ID of the instance type cannot be empty. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceCpus |You've reached the limit on the number of instance CPU that you can create, please submit ticket to request an increase in quota. |The quota of instance CPU number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceTypeInstances |You've reached the limit on the number of instance type instances that you can create, please submit ticket to request an increase in quota. |The quota of the specified instance type you can create is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumLocalVolumeCpus |You've reached the limit on the number of local volume instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu] quota. |The CPU quota of the Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGeneralCpus |You've reached the limit on the number of general reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu_ri_regional] quota. |The CPU quota of the general\-purpose instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic_ri_regional] quota. |The GPU card quota of regional RIs that can be used for purchasing GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance_ri_regional] quota. |The GPU card quota for HPC\-optimized instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus |You've reached the limit on the number of local volume reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu_ri_regional] quota. |The CPU quota of regional RIs that can be used for purchasing Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |InvalidImage.InstanceTypeMismatch |The specified image and instance type do not match. |The specified image does not support the specified instance type. |
|412 |InvalidInstance.Expired |The specified instance has expired. |The instance has expired. |
|412 |OperationDenied.InstanceHasUnfinishedOrder |The specified operation is denied as your instance has unfinished orders. |The specified operation is rejected because there are pending orders associated with the instance. |
|412 |OperationDenied.InstanceIsCreatingImage |The specified operation is denied as your instance is creating image. |The specified operation is rejected because the instance is being used to create a custom image. |
|412 |OperationDenied.InstanceIsSnapshotRollback |The specified operation is denied as your instance is rolling back snapshot. |The specified operation is rejected because the instance is rolling back to a snapshot. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The resources are currently insufficient. Try again later or select other instance types. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
