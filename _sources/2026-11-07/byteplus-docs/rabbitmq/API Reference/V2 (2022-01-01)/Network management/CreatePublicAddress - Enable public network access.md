---
title: "CreatePublicAddress - Enable public network access"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/CreatePublicAddress_-_Enable_public_network_access"
---

Call the CreatePublicAddress API to enable public network access for the RabbitMQ instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If public network access is not enabled when creating the instance, you can call this API to bind an Elastic IP (EIP) after creating the instance to enable public network access. The EIP provides independent public IP resources, including the public IP address and outbound bandwidth service. The public address will bind to your Elastic Public IP (EIP). Fees are charged by the EIP.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 100 times/second; the per\-user request frequency limit is 20 times/second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreatePublicAddress&groupName=%E7%BD%91%E7%BB%9C%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|4ocIdF">必选</span> `Example value: CreatePublicAddress`

The action to execute, valid value: CreatePublicAddress.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|LKsbM4">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**EipId** <span data-label="purple">string</span> <span data-api-tag="require|mDZvDU">必选</span> `Example value: eip-2zeujxs*****6cd`

EIP ID.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|TyQZmN">必选</span> `Example value: rbtmq-5b293870****`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=CreatePublicAddress&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-9283a61f****",
   "EipId": "eip-36sveyn9wy39c383g0wbs****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "2023021717563303023552D2E1FF86C7F6",
        "Action": "CreatePublicAddress",
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
|400 |InvalidParameter |The specified parameter %s is not valid. |Parameter value %s is invalid. |
|400 |MissingParameter |The request body is missing a required parameter %s. |Missing %s parameter. |
|403 |OperationDenied.InternetAccessEnabled |Internet access is enabled for the instance. |This instance has public network access enabled. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this operation. |
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |Backend task is running, please try again later. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |Instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
