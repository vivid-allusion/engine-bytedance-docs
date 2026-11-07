---
title: "DeleteInstance - Delete instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DeleteInstance_-_Delete_instance"
---

Call the DeleteInstance API to release pay\-as\-you\-go instances.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Deleting instances is typically used in scenarios such as application decommissioning.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The RabbitMQ instance is in <strong>Running</strong> or <strong>Fault</strong> status.</div>


* <div data-tips="true" data-tips-type="tip">The related Queue, Exchange, and Vhost of the RabbitMQ instance have been deleted.</div>


* <div data-tips="true" data-tips-type="tip">Instances cannot be recovered once deleted. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">Only pay\-as\-you\-go instances support deletion through this API. Subscription instances are automatically deleted upon expiration and can not be deleted during the contract period.</div>



<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteInstance&groupName=%E5%AE%9E%E4%BE%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|ydYUVM">必选</span> `Example value: DeleteInstance`

The action to perform, valid value: DeleteInstance.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|QDiB1R">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|CH0NYs">必选</span> `Example value: rbtmq-5b293870****`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DeleteInstance&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
    "InstanceId": "rbtmq-bdb8a520****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230217173733D983590860194F946E92",
        "Action": "DeleteInstance",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": null
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |A background task is running. Please try again later. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance state does not allow this action. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
