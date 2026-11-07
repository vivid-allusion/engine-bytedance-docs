---
title: "ModifyInstanceAttributes - Modify instance information"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/ModifyInstanceAttributes_-_Modify_instance_information"
---

Call the ModifyInstanceAttributes API to change the instance name, description, and other instance information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to **100 times/second**; per\-user request frequency limit is **20 times/second**.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceAttributes&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|6sAwbb">必选</span> `Example value: ModifyInstanceAttributes`

Operation to perform, value: ModifyInstanceAttributes.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|R8zI7t">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|6R2OQ6">必选</span> `Example value: rbtmq-5b293870****`

Instance ID.



**InstanceName** <span data-label="purple">string</span> `Optional` `Example value: test-instance`

Instance name.



**InstanceDescription** <span data-label="purple">string</span> `Optional` `Example value: instance for test mqtt`

Instance description.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=ModifyInstanceAttributes&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-9283a61f****",
   "InstanceName": "test-instance",
   "InstanceDescription": "instance for test"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230217173733D983590860194F946E92",
        "Action": "ModifyInstanceAttributes",
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
|400 |InvalidParameter |The specified parameter %s is not valid. |The parameter value %s is invalid. |
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You are not authorized yet. Authorize or switch accounts and try again. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance state does not allow this operation. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |Instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
