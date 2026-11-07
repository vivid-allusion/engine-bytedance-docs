---
title: "StopInstance - Stops an instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/StopInstance"
---

Call the StopInstance operation to stop an instance.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

Only instances in the **Running** state can be stopped.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Stopping an instance will interrupt your business operations. Please proceed with caution.

* To stop billing, you need to delete the instance and its [associated ](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances)resources.

* After a spot instance is stopped, you cannot restart it if the resources are insufficient.

* Stopping a subscription instance does not affect the expiration time.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=StopInstance&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|SX6A3n">必选</span> `Sample value: StopInstance`

The operation that you want to perform. Valid value: StopInstance.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|9pdcK3">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client automatically generates a token to ensure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to only precheck this request. Value:


* true: Sends a check request without stopping the instance. Check items include: whether required parameters are specified, request format, business restrictions, and ECS inventory. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

* false (default): Sends a normal request and directly shuts down the instance after the check is passed.



**ForceStop ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to forcibly shut down the instance. Valid values:


* true: Forcibly shuts down the instance. It is equivalent to a typical power\-off operation, and all cached data that has not been written to the storage device will be lost.

* false (default): Normal shutdown.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the following types of instances, regardless of whether <code>ForceStop</code> is set to <code>true</code> or <code>false</code>, the instances will be forcibly shut down.</div>



* <div data-tips="true" data-tips-type="tip">EBM instances.</div>


* <div data-tips="true" data-tips-type="tip">HPC\-optimized ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2 instances.</div>


> <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2 instances are currently in Beta. If you need a trial, please contact your account manager.</div>




**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|I0MOTq">必选</span> `Sample value: i-3tiefmkskq3vj0x0****`

The instance ID.



**StoppedMode ** <span data-label="purple">string </span>`Optional` `Sample value: KeepCharging`

The shutdown mode: Valid values:


* KeepCharging: Normal Mode. After the instance is stopped, it and its associated resources are retained, and you are charged for them in the same way as before the stop.

* StopCharging: Economical Mode. After the instance is stopped, its computing resources (vCPU, GPU, and memory) will be reclaimed and billing will stop. The mounted volumes, images, and EIPs are retained and you are charged for them.

   For the conditions for enabling Economical Mode, see [Economical mode for pay-as-you-go instances](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances).


Default value: If you [set the default shutdown mode for the instance to Economical Mode](https://docs.byteplus.com/en/docs/ecs/Economical_mode_for_pay-as-you-go_instances-1#.5byA5ZCv6buY6K6k6IqC55yB5YGc5py65qih5byP) in the ECS console and the conditions for enabling Economical Mode are met, the default value of this parameter is `StopCharging`. Otherwise, the default value is `KeepCharging`.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=StopInstance&Version=2020-04-01&InstanceId=i-3tiefmkskq3vj0****** HTTP/1.1
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
        "Action": "StopInstance",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in the current status does not support this action. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidStoppedMode.Malformed |The specified StoppedMode is malformed. |The specified StoppedMode is invalid. |
|400 |InvalidStoppedModeForAffinityGroupInstance.Unsupported |The specified affinity group instance does not support stop charging. |The specified affinity group instance does not support Economical Mode. |
|400 |InvalidStoppedModeForScheduledInstance.Unsupported |The specified scheduled instance does not support stop charging. |The specified ESI does not support Economical Mode. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceIds cannot be left empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|409 |InvalidStoppedMode.Conflict |The specified StoppedMode conflicts with instance status. |StoppedMode conflicts with the instance status. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |InvalidStoppedMode.ChargeTypeMismatch |The specified StopCharging does not match the instance's ChargeType. |The current billing method of the instance does not support economical mode. |
|412 |InvalidStoppedMode.InstanceTypeMismatch |The specified StopCharging does not match the instance's InstanceType. |The current instance type does not support Economical Mode. |
|412 |OperationDenied.InstanceIsCreatingImage |The specified operation is denied as your instance is creating image. |The specified operation is rejected because the instance is being used to create a custom image. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The resources are currently insufficient. Try again later or select other instance types. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
