---
title: "RebootInstance - Restarts an instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/RebootInstance"
---

Call the RebootInstance operation to restart an instance.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

Only ECS instances in the **Running** state can be restarted.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Restarting a bare metal instance using this operation may result in instance data loss. Complete the restart operation in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

* Restarting an instance will interrupt your business for a short period of time. Proceed with caution.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RebootInstance&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|bx9TdZ">必选</span> `Sample value: RebootInstance`

The operation that you want to perform. Value: RebootInstance.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|d8kq0T">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specifies whether to only precheck this request.


* true: Sends a check request without restarting the instance. Check items include whether the required parameters are provided, the request format, and business limits. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

* false (default): Sends a normal request and directly restarts the instance after the check is passed.



**ForceStop ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to forcibly shut down the instance before restarting the instance. Valid values:


* true: Forcibly shuts down the instance. It is equivalent to a typical power\-off operation, and all cached data that has not been written to the storage device will be lost.

* false (default): Normal shutdown.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the following types of instances, regardless of whether <code>ForceStop</code> is set to <code>true</code> or <code>false</code>, the instances will be forcibly shut down.</div>



* <div data-tips="true" data-tips-type="tip">EBM instances.</div>


* <div data-tips="true" data-tips-type="tip">HPC\-optimized ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2 instances.</div>


> <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">ebmhpcpni2l, ebmhpcpni2, and ebmhpchfpni2 instances are currently in Beta. If you need a trial, please contact your account manager.</div>




**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|OAsudk">必选</span> `Sample value: i-3tiefmkskq3vj0x0****`

The instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=RebootInstance&Version=2020-04-01&InstanceId=i-3tiefmkskq3vj0****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20210623195036010225145152013****",
        "Action": "RebootInstance",
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
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in current status does not support this action. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceId cannot be left empty. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |OperationDenied.InstanceIsCreatingImage |The specified operation is denied as your instance is creating image. |The specified operation is rejected because the instance is being used to create a custom image. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
