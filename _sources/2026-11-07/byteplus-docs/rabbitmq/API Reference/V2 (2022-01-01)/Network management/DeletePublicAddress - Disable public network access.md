---
title: "DeletePublicAddress - Disable public network access"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DeletePublicAddress_-_Disable_public_network_access"
---

Call the DeletePublicAddress API to disable public network access.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If you no longer need to access the instance via the public network, use this API to disable public network access and unbind the Elastic IP address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To change the instance's Elastic IP, first disable public network access using this API, then call EnableInternetAccess to enable public network access and bind the new Elastic IP address.</div>


* <div data-tips="true" data-tips-type="tip">This API can dynamically disable the instance's public network access but does not release the Elastic IP resource. You need to release the Elastic IP manually.</div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 100 times/second. The per\-user request frequency limit is 20 times/second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeletePublicAddress&groupName=%E7%BD%91%E7%BB%9C%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|PkDjmN">必选</span> `Example value: DeletePublicAddress`

The action to perform, value: DeletePublicAddress.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|J9Bn0E">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|5cI4IB">必选</span> `Example value: rbtmq-5b293870****`

The RabbitMQ instance ID with public network access to be disabled.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DeletePublicAddress&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-9283a61f****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "202302171758012E56A0172D79CA886DB1",
        "Action": "DeletePublicAddress",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

Error codes

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Specifications |
|---|---|---|---|
|403 |OperationDenied.InternetAccessDisabled |Internet access is disabled for the instance. |This instance does not have public network access enabled. |
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |The background task is running. Please try again later. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this action. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
