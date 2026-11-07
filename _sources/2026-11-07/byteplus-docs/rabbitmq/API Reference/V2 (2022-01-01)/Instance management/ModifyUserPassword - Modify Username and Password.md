---
title: "ModifyUserPassword - Modify Username and Password"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/ModifyUserPassword_-_Modify_Username_and_Password"
---

Call the ModifyUserPassword interface to reset the administrator account password for the RabbitMQ instance Web UI.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

For security, RabbitMQ version recommends regularly maintaining the administrator account password for the Web UI. If you forget the administrator username or password, you can reset the account and password using this interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This interface limits requests to 20 times per second; the per\-user request frequency is limited to 5 times per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyUserPassword&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this interface and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|j7ajx5">必选</span> `Example value: ModifyUserPassword`

Action to perform, value: ModifyUserPassword.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|6zPEis">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|ywqwr0">必选</span> `Example value: rbtmq-2f707884****`

Instance ID.



**UserName** <span data-label="purple">string</span> <span data-api-tag="require|JpbbFS">必选</span> `Example value: admin`

The administrator username that requires password modification.



**Password** <span data-label="purple">string</span> <span data-api-tag="require|0YOmQq">必选</span> `Example: Admin****`

Account password. Must meet the following requirements:


* 8 to 32 characters.

* Include at least three of the following: uppercase letters, lowercase letters, numbers, special characters.

* Special characters include `!@#$%^&\*()_+-=`.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=ModifyUserPassword&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-2f707884****",
   "UserName": "testcase2312312",
   "Password":"Admin******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230220215437B5837F4C4321FCD0AF2A",
        "Action": "ModifyUserPassword",
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


|Status code |Error code |Error message |Specifications |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The parameter value %s is invalid. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance state does not allow this action. |
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |Background tasks are running, please try again later. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
