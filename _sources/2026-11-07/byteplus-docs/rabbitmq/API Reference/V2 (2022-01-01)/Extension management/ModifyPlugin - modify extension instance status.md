---
title: "ModifyPlugin - modify extension instance status"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/ModifyPlugin_-_modify_extension_instance_status"
---

Call the ModifyPlugin API to enable or disable the extension.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: this API limits requests to **20 times/second**; the per\-user request frequency limit is **5 times/second**.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyPlugin&groupName=%E6%8F%92%E4%BB%B6%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|hrovBj">必选</span> `Example value: ModifyPlugin`

Action to perform, value: ModifyPlugin.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|xh6isM">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|aJ1fB7">必选</span> `Example value: rbtmq-*******`

Instance ID.



**Plugins** <span data-label="purple">object[]</span> <span data-api-tag="require|fwhOc7">必选</span> `Example value: [ { "PluginName": "rabbitmq_delayed_message_exchange", "Enabled": true }, { "PluginName": "rabbitmq_tracing", "Enabled": true } ]`

List of extensions pending modification.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Extensions not specified in the list will not have their status adjusted.</div>



**PluginName** <span data-label="purple">string</span> <span data-api-tag="require|CPUOPf">必选</span> `Example value: rabbitmq_mqtt`

Extension name. Supports the following settings:


* rabbitmq_mqtt: Indicates whether the instance supports the MQTT protocol (TCP mode).

* rabbitmq_web_mqtt: Indicates whether the instance supports the MQTT protocol (WebSocket mode).

* rabbitmq_delayed_message_exchange: Indicates whether the instance enables the message delay function. The extension delay time has an error margin of about 1%. It may send messages to consumers earlier or later than expected.

* rabbitmq_stomp: Indicates whether the instance supports the STOMP protocol.

* rabbitmq_tracing: Indicates whether the tracing extension is enabled.

* rabbitmq_consistent_hash_exchange: Indicates whether the consistent hash exchange is enabled.

* rabbitmq_shovel: Indicates whether the instance enables the shovel plugin. The shovel plugin supports automatic and reliable message transfer between different RabbitMQ servers.

* rabbitmq_shovel_management: Indicates whether the instance enables the shovel management plugin. The plugin supports managing and monitoring shovel's configuration and status. If enabled, please use it in the WebUI console.

* rabbitmq_federation: Indicates whether the instance enables the RabbitMQ Federation plugin. The Federation plugin is used to transfer messages between brokers or clusters.

* rabbitmq_federation_management：Indicates whether the instance enables the RabbitMQ Federation management plugin. The plugin provides a GUI for Federation functions.



**Enabled** <span data-label="purple">boolean</span> <span data-api-tag="require|nNNKwI">必选</span> `Example value: true`

Whether to enable the extension. Default value: false


* true: enable the extension.

* false: disable the extension.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=ModifyPlugin&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-2f707884****",
   "Plugins": {
        "PluginName": "rabbitmq_mqtt",
        "Enabled": true
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202302171758012E56A0172D79CA886DB1",
        "Action": "ModifyPlugin",
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
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |Background task is running, please try again later. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this operation. |
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
