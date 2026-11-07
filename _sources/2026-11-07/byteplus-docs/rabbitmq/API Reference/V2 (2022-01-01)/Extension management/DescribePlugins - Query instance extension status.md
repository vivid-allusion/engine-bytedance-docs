---
title: "DescribePlugins - Query instance extension status"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DescribePlugins_-_Query_instance_extension_status"
---

Call the DescribePlugins API to query the extension list of a specified instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API retrieves the extension list for a specified instance, including currently supported extensions, each extension's enable status, and related notes. Before changing an extension's enable status, check its details through this API, such as whether enabling an extension will trigger a Restart of the instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Notes\nRequest frequency: This API limits requests to **100 times/second**; the per\-user request frequency limit is **20 times/second**.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribePlugins&groupName=%E6%8F%92%E4%BB%B6%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|GIJVyy">必选</span> `Example value: DescribePlugins`

Operation to execute, valid value: DescribePlugins



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ffqoq5">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|nF9ZRi">必选</span> `Example value: rbtmq-2f707884****`

Instance ID.



**PageSize** <span data-label="purple">integer</span> <span data-api-tag="require|OPivgX">必选</span> `Example value: 10`

This parameter indicates the amount of data per page when displaying query results with pagination. Value range: 1 to 100.



**PageNumber** <span data-label="purple">integer</span> <span data-api-tag="require|WnBxnE">必选</span> `Example value: 1`

This parameter represents the page number when displaying paginated query results. The minimum supported value is 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId** <span data-label="purple">string</span> `Example value: rbtmq-*******`

Instance ID.



**Total** <span data-label="purple">integer</span> `Example value: 3`

Total number of extensions.



**PluginsInfo** <span data-label="purple">object[]</span> `Example value: /`

Plugin information for the instance, including the list of supported extensions and the enable status of each extension.


**EnablePrompt** <span data-label="purple">string</span> `Example value: enabling this extension triggers a RabbitMQ Cluster rolling restart`

Description of precautions for enabling this extension.



**PluginName** <span data-label="purple">string</span> `Example value: rabbitmq_mqtt`

Extension name.



**Version** <span data-label="purple">string</span> `Example value: 3.8.18`

Extension version.



**NeedRebootOnChange** <span data-label="purple">boolean</span> `Example value: true`

Enabling or disabling the extension triggers RabbitMQ instance Restart.


* true: the instance will Restart.

* false: the instance will not Restart.



**Enabled** <span data-label="purple">boolean</span> `Example value: true`

Whether the extension is enabled.


* true: extension is enabled.

* false: extension is disabled.



**Port** <span data-label="purple">integer</span> `Example value: 8883`

Extension service port.



**DisablePrompt** <span data-label="purple">string</span> `Example: disabling this extension will trigger a RabbitMQ Cluster rolling Restart`

Precaution descriptions on disabling this extension.



**Description** <span data-label="purple">string</span> `Example value: supports MQTT protocol (TCP mode)`

Description of the extension.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DescribePlugins&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-2f707884****",
   "PageSize": "10",
   "PageNumber": "1"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
"Result": {
        "InstanceId": "rbtmq-2f707884****",
        "PluginsInfo": [
            {
"Description": "Supports MQTT protocol (TCP mode)",
"DisablePrompt": "Disabling this extension will trigger a RabbitMQ cluster rolling restart",
"EnablePrompt": "Enabling this extension will trigger a RabbitMQ cluster rolling restart",
                "Enabled": true,
                "NeedRebootOnChange": true,
                "PluginName": "rabbitmq_mqtt",
                "Port": 8883,
                "Version": "3.8.18"
            },
            {
"Description": "Supports MQTT protocol (WebSocket mode)",
"DisablePrompt": "Disabling this extension will trigger a RabbitMQ cluster rolling restart",
"EnablePrompt": "Enabling this extension will trigger a RabbitMQ cluster rolling restart",
                "Enabled": false,
                "NeedRebootOnChange": true,
                "PluginName": "rabbitmq_web_mqtt",
                "Port": 15676,
                "Version": "3.8.18"
            },
            {
"Description": "delayed message",
"DisablePrompt": "disabling this extension will result in the loss of undelivered delayed messages",
                "EnablePrompt": "",
                "Enabled": false,
                "NeedRebootOnChange": false,
                "PluginName": "rabbitmq_delayed_message_exchange",
                "Port": 0,
                "Version": "3.8.17"
            },
            {
"Description": "Supports the Stomp protocol",
"DisablePrompt": "Disabling this extension will trigger a RabbitMQ cluster rolling restart",
"EnablePrompt": "Enabling this extension will trigger a RabbitMQ cluster rolling restart",
                "Enabled": false,
                "NeedRebootOnChange": true,
                "PluginName": "rabbitmq_stomp",
                "Port": 61614,
                "Version": "3.8.18"
            },
            {
"Description": "Tracks the inflow and outflow of messages and records them in log files. Ensure sufficient instance storage capacity. After enabling, access the WebUI console to use it.",
"DisablePrompt": "Disabling this extension will prevent message tracking.",
                "EnablePrompt": "",
                "Enabled": false,
                "NeedRebootOnChange": false,
                "PluginName": "rabbitmq_tracing",
                "Port": 0,
                "Version": "3.8.18"
            },
            {
"Description": "Consistent hash exchange routes messages to queues using a consistent hash algorithm.",
"DisablePrompt": "Disabling this extension will prevent the use of the consistent hash Exchange.",
                "EnablePrompt": "",
                "Enabled": true,
                "NeedRebootOnChange": false,
                "PluginName": "rabbitmq_consistent_hash_exchange",
                "Port": 0,
                "Version": "3.8.18"
            }
        ],
        "Total": 6
    }

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

Error codes

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this operation. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |Instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
