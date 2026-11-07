---
title: "DeleteInstance - Deletes an instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteInstance"
---

Call the DeleteInstance operation to delete an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Only pay\-as\-you\-go instances (including spot instances and Elastic Scheduled Instances) or subscription instances that have expired or been unsubscribed can be deleted.

   * After a pay\-as\-you\-go instance and the associated resources are deleted, its billing stops. [Why is a deleted instance still being billed?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5Li65LuA5LmI5a6e5L6L5bey57uP5Yig6Zmk77yM5L2G5LuN54S25Zyo6K6h6LS577yf)

   * A subscription instance cannot be deleted before it [expires](https://docs.byteplus.com/en/docs/ecs/Expiration) or is [unsubscribed](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO). You can convert the instance to a pay\-as\-you\-go instance and manually delete it, or manually delete it within the resource retention period after the instance expires or is unsubscribed. If an instance is not renewed after expiration or unsubscription, it will be automatically released.

* For details on the retention of resources related to an instance after the instance is deleted, see [Status of instance resources after an ECS instance is deleted](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances#.5Yig6Zmk5ZCO5a6e5L6L55u45YWz6LWE5rqQ5oOF5Ya1).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteInstance&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Sample value: DeleteInstance`

The operation that you want to perform. Valid value: DeleteInstance.



**Version ** <span data-label="purple">string   </span>`Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional Sample value: false`

Specifies whether to precheck this request. Valid values:


* true: Sends a check request without deleting the instance. Check items include whether required parameters are filled, request format, and business restrictions. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

* false (default): Sends a normal request and directly deletes the instance after the check is passed.



**InstanceId ** <span data-label="purple">string   </span>`Sample value: i-3thhlu8byl4bwbha****`

The instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteInstance&Version=2020-04-01&InstanceId=i-3thhlu8byl4bwb****** HTTP/1.1
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
        "Action": "DeleteInstance",
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
|400 |InvalidChargeType |The specified ChargeType is not valid, is unsupported, or cannot be used. |The specified instance billing method is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in current status does not support this action. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceIds cannot be left empty. |
|403 |InvalidOperation.DeletionProtection |The operation is not allowed due to deletion protection. |This operation is not supported because the instance release protection is enabled. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |OperationDenied.AffinityGroupInstance |The specified operation is denied as your instance is an affinity group instance, and all instanceIds the affinity group must be specified. |The specified operation is rejected because the instance is an affinity group instance, and you must specify the IDs of all instances in the affinity group. |
|412 |OperationDenied.InstanceHasUnfinishedOrder |The specified operation is denied as your instance has unfinished orders. |The specified operation is rejected because there are pending orders associated with the instance. |
|412 |OperationDenied.InstanceIsCreatingImage |The specified operation is denied as your instance is creating image. |The specified operation is rejected because the instance is being used to create a custom image. |
|412 |OperationDenied.InstanceIsSnapshotRollback |The specified operation is denied as your instance is rolling back snapshot. |The specified operation is rejected because the instance is rolling back to a snapshot. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
