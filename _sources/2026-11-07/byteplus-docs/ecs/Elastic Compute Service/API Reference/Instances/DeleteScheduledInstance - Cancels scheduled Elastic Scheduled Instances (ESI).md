---
title: "DeleteScheduledInstance - Cancels scheduled Elastic Scheduled Instances (ESI)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteScheduledInstance"
---

Call the DeleteScheduledInstance operation to cancel an ESI reservation.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Whether you can cancel an ESI order depends on the ESI type. For more information, see the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>



|Type ||Is reservation cancellation supported? |
|---|---|---|
|ESI ||An ESI order can be cancelled within 30 minutes after it is created. |
|ESI\-Segmented |Scheduled delivery (Reserve) |You can cancel an ESI order before the instances specified in the order are delivered, that is, before the start time of the resource delivery time slot. |
||Immediate delivery (Immediate) |Reservation cancellation is not supported. |


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteScheduledInstance&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|FmyuTe">必选</span> `Sample value: DeleteScheduledInstance`

The operation that you want to perform. Valid value: DeleteScheduledInstance.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|TaOJ6H">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**ScheduledInstanceId** <span data-label="purple">string</span> <span data-api-tag="require|TEgckG">必选</span> `Sample value: esi-3thhlu8byl4bwbha****`

ESI order ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteScheduledInstance&Version=2020-04-01&ScheduledInstanceId=esi-3thhlu8byl4bwbha**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240104191846FF4457331417A963****",
        "Action": "DeleteScheduledInstance",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing",
        "Error": {
            "Code": "InvalidDeliveryTypeForScheduledInstanceDeletion.Unsupported",
            "Message": "The specified DeliveryType cannot be used for scheduled instance deletion."
        }
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
|400 |InvalidDeliveryTypeForScheduledInstanceDeletion.Unsupported |The specified DeliveryType cannot be used for scheduled instance deletion. |You cannot cancel an ESI order with immediate delivery specified. |
|400 |InvalidScheduledInstanceStatus |The specified scheduled instance is not in the correct status for the request. |The ESI order in the current status does not support this action. |
|400 |MissingParameter.ScheduledInstanceId |The required parameter ScheduledInstanceId is not supplied. |The parameter ScheduledInstanceId cannot be empty. |
|404 |InvalidScheduledInstance.NotFound |The specified scheduled instance does not exist. |The specified ESI order does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |OperationDenied.LatestCancelTime |The specified operation is denied as your resource has exceeded the latest appointment cancellation time. |The specified operation is rejected because the latest deadline for canceling the reservation has passed for your resources. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
