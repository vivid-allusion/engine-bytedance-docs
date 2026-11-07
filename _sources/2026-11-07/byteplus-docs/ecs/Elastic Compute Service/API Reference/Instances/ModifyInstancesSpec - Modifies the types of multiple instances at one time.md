---
title: "ModifyInstancesSpec - Modifies the types of multiple instances at one time"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstancesSpec"
---

Call the ModifyInstancesSpec operation to modify the types of the specified instances at one time.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* If the current instance type fails to meet your application requirements or exceeds them, you can first check the available instance type change options for your instance by referring to [Instance types supporting type change](https://docs.byteplus.com/en/docs/ecs/Overview-2). Then, modify the instance type (including vCPU and memory). Both upgrades and downgrades are supported.

* For precautions and usage limits related to changing the instance type, see [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstancesSpec&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|WetDUa">必选</span> `Sample value: ModifyInstancesSpec`

The operation that you want to perform. Valid value: ModifyInstancesSpec.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|r5hKMJ">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|FYiotn">必选</span> `Sample value: InstanceIds.1=i-3ti9101aju3vj0******&InstanceIds.2=i-3tiegs1y963vj0******`

The instance ID. Up to 20 instance IDs are supported.

Argument \- N: specifies the serial number of the instance.

Multiple instance IDs are separated by &.



**InstanceTypeId** <span data-label="purple">string</span> <span data-api-tag="require|maWJvb">必选</span> `Sample value: ecs.g3il.large`

The new instance type.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error message for the instance being operated on.


**Code** <span data-label="purple">string</span> `Sample value: InvalidInstance.NotFound`

The error code for the failure of a specific individual request during batch operations. Value:


* MissingParameter.InstanceId: The instance ID cannot be empty.

* InvalidInstance.NotFound: The specified instance does not exist.

* InternalError: An internal error occurred. Try again. If multiple attempts fail, submit a ticket.

* OperationDenied.ResourceCreatedByOtherService: The specified operation is rejected because your resource has been created by another service. You can query the corresponding service based on the system tag of the resource.

* InvalidInstanceTypeForConfidentialComputing.NotSupported: The specified instance type does not support confidential computing capabilities.

* LimitExceeded.MaximumVolumes: The number of volumes mounted to the specified instance exceeds the upper limit.

* InvalidInstanceStatus: The current status of the instance does not support this operation.

* OperationDenied.InstanceIsCreatingImage: The specified operation is rejected because the instance is being used to create a custom image.

* OperationDenied.InstanceIsSnapshotRollback: The specified operation is rejected because the instance is rolling back to a snapshot.

* InvalidInstanceType: The specified instance type is invalid.

* InvalidSpotStrategyForModifyInstanceSpec.Unsupported: The spot policy of the specified instance does not support instance type changes.

* InvalidScheduledInstanceForModifyInstanceSpec.Unsupported: The specified Elastic Scheduled Instance (ESI) does not support instance type changes.

* InvalidInstance.Expired: The instance has expired.

* InvalidInstanceForResizeTypeFamily.Unsupported: The specified instance does not support instance type changes across instance type families.

* InvalidInstanceForDowngradeSpec.Unsupported: The specified instance cannot be downgraded.

* LimitExceeded.MaximumHighPerformanceNetworkInterfaces: The number of network interfaces in RDMA communication mode associated with the specified instance exceeds the upper limit.

* InvalidAffinityGroupInstanceForModifyInstanceSpec.Unsupported: The specified instance is an affinity group instance, which does not support instance type changes.

* LimitExceeded.MaximumInstancePrivateIpsPerNetworkInterface: The number of secondary private IP addresses of the specified network interface exceeds the upper limit of the instance type.

* LimitExceeded.MaximumNetworkInterfaces: The number of network interfaces mounted to the specified instance exceeds the upper limit.

* InvalidImage.InstanceTypeMismatch: The specified image does not support the specified instance type.

* OperationDenied.InstanceHasUnfinishedOrder: The specified operation is rejected because there are pending orders associated with the instance.

* OperationDenied.ResourceLocked: The specified operation is rejected because your resource has been locked by another operation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified instance does not exist.`

The error information for the failure of a specific individual request during batch operations. Value:


* The required parameter InstanceId is not supplied.

* The specified instance does not exist.

* An internal error has occurred.

* The specified operation is denied as your resource is created by other service. You can check system tags to find the service.

* The specified instance type not support confidential computing.

* You've reached the limit on the number of volumes that can be attached to the instance.

* The status of the specified instance does not support this request.

* The specified operation is denied as your instance is creating image.

* The specified operation is denied as your instance is rolling back snapshot.

* The specified InstanceType is invalid.

* The specified SpotStrategy cannot be used to modify instance specification.

* The specified scheduled instance cannot be used to modify instance specification.

* The specified instance has expired.

* The specified instance does not support changing instance specifications across specification families.

* The specified instance does not support downgrade instance specifications.

* You've reached the limit on the number of HighPerformance NetworkInterfaces that can be attached to the instance.

* The specified affinity group instance does not support modify instance specification.

* The number of specified PrivateIpsPerNetworkInterface exceeds the maximum limit of the instance specification.

* You've reached the limit on the number of NetworkInterfaces that can be attached to the instance.

* The specified image and instance type do not match.

* The specified operation is denied as your instance has unfinished orders.

* The specified operation is denied as your resource is locked for another operation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>





**InstanceId** <span data-label="purple">string</span> `Sample value: i-ybo349sxoncm9t******`

The ID of the instance on which the operation is performed.




**OrderId** <span data-label="purple">string</span> `Sample value: Order7021038849342******`

The order number.

When you set `InstanceChargeType` =to `PrePaid`, this parameter is returned.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstancesSpec&Version=2020-04-01&InstanceIds.1=i-3ti9101aju3vj0******&InstanceIds.2=i-3tiegs1y963vj0******&InstanceTypeId=ecs.g3il.large HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "ModifyInstancesSpec",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order7021038849342******",
        "OperationDetails": [
            {
                "InstanceId": "i-ahipakt2gcg95jpv****",
                "Error": null
            },
            {
                "InstanceId": "i-ahipakt2gdg95lbe****",
                "Error": {
                    "Code": "InvalidInstance.NotFound",
                    "Message": "The specified instance does not exist."
                }
            }
        ]
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
|400 |InvalidAffinityGroupInstanceForModifyInstanceSpec.Unsupported |The specified affinity group instance does not support modify instance specification. |The specified instance is an affinity group instance, which does not support instance type changes. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostInstanceForModifyInstanceSpec.Unsupported |The specified instance is on dedicated host, cannot be used to modify instance specification. |The specified instance is on a dedicated host, which does not support instance type changes. |
|400 |InvalidInstanceChargeType.Conflict |The ChargeTypes of the specified instances are different. |The billing methods of the specified instances are inconsistent. |
|400 |InvalidInstanceForDowngradeSpec.Unsupported |The specified instance does not support downgrade instance specifications. |The specified instance does not support downgrade. |
|400 |InvalidInstanceForResizeTypeFamily.Unsupported |The specified instance does not support changing instance specifications across specification families. |The specified instance does not support instance type changes across instance type families. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceType |The specified InstanceType is invalid. |The specified instance type is invalid. |
|400 |InvalidInstanceType.Conflict |The InstanceTypes of the specified instances are different. |The instance types of the specified instances are inconsistent. |
|400 |InvalidScheduledInstanceForModifyInstanceSpec.Unsupported |The specified scheduled instance cannot be used to modify instance specification. |The specified Elastic Scheduled Instance (ESI) does not support instance type changes. |
|400 |InvalidSpotStrategyForModifyInstanceSpec.Unsupported |The specified SpotStrategy cannot be used to modify instance specification. |The spot policy of the specified instance does not support instance type changes. |
|400 |InvalidZoneId.Conflict |The ZoneIds of the specified instances are different. |The availability zones of the specified instances are inconsistent. |
|400 |LimitExceeded.MaximumBranchNetworkInterfaces |You've reached the limit on the number of branch enis that can be attached to a single instance. |The number of branches for the specified instance exceeds the upper limit. |
|400 |LimitExceeded.MaximumHighPerformanceNetworkInterfaces |You've reached the limit on the number of HighPerformance NetworkInterfaces that can be attached to the instance. |The number of network interfaces in RDMA communication mode associated with the specified instance exceeds the maximum limit. |
|400 |LimitExceeded.MaximumInstanceIds |You've reached the limit on the number of InstanceIds that you can set. |The specified number of InstanceIds exceeds the maximum limit. |
|400 |LimitExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of NetworkInterfaces that can be attached to the instance. |The specified number of network interfaces associated with the instance exceeds the maximum limit. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be left empty. |
|400 |MissingParameter.InstanceTypeId |The required parameter InstanceTypeId is not supplied. |The ID of the instance type cannot be empty. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceCpus |You've reached the limit on the number of instance CPU that you can create, please submit ticket to request an increase in quota. |The quota of instance CPU number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceTypeInstances |You've reached the limit on the number of instance type instances that you can create, please submit ticket to request an increase in quota. |The quota for the specified instance type you can create is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumLocalVolumeCpus |You've reached the limit on the number of local volume instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu] quota. |The CPU quota of the Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGeneralCpus |You've reached the limit on the number of general reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu_ri_regional] quota. |The CPU quota of the general\-purpose instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic_ri_regional] quota. |The GPU card quota of regional RIs that can be used for purchasing GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance_ri_regional] quota. |The GPU card quota for HPC\-optimized instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus |You've reached the limit on the number of local volume reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu_ri_regional] quota. |The CPU quota of regional RIs that can be used for purchasing Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |Your specified resource is no longer accessible because your BytePlus account has violated relevant regulations. To restore service access, submit a ticket to contact our service team for assistance. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
|412 |InvalidImage.InstanceTypeMismatch |The specified image and instance type do not match. |The specified image does not support the specified instance type. |
|412 |InvalidInstance.Expired |The specified instance has expired. |The instance has expired. |
|412 |OperationDenied.InstanceHasUnfinishedOrder |The specified operation is denied as your instance has unfinished orders. |The specified operation is rejected because there are pending orders associated with the instance. |
|412 |OperationDenied.InstanceIsCreatingImage |The specified operation is denied as your instance is creating image. |The specified operation is rejected because the instance is being used to create a custom image. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified action was rejected because your resource has been locked by other actions. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The capacity resources are currently insufficient. Please try again later or select other instance types. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
