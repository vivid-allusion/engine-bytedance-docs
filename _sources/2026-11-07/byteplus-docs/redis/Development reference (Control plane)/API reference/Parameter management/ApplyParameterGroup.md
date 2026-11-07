---
title: "ApplyParameterGroup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/ApplyParameterGroup"
---

Call the ApplyParameterGroup API to apply the parameter template to the instance.

## Request type

Asynchronous request.

## Precautions

* The database version of the target instance should be consistent with the parameter template database version to be applied. For example, if the parameter template supports Redis database version 6.0, then the parameter template only supports instances applied for Redis version 6.0.

* If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ApplyParameterGroup&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|ParameterGroupId |String |Yes |pg\-cnlfm5yzmxehmkw\*\*\*\* |Parameter templates ID. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ApplyParameterGroupInfo |Object of [InstanceApplyParameterGroupInfo](https://docs.byteplus.com/en/docs/55/118245#instanceapplyparametergroupinfo) |Refer to the Sample response. |Show the differences between the parameter template and the instance's current parameter configuration. |

### InstanceApplyParameterGroupInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|ApplyParameters |Array of [ParameterInfo](https://docs.byteplus.com/en/docs/55/118245#parameterinfo) |Refer to the Sample response. |List of parameter information to apply. |
|ParameterGroupId |String |pg\-cnlfm5yzmxehmkw\*\*\*\* |Parameter templates ID. |

### ParameterInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CurrentValue |String |100 |The running value of this parameter in the parameter template. |
|Description |String |Minimum fragmented space to trigger memory defragmentation. Unit: MB, value range 100–1024. |Parameter description. |
|NeedReboot |Boolean |false |Whether an instance restart is required for the modification to take effect. Valid values:<br><br><br>* `true`: requires restart.<br><br>* `false`: No restart required. |
|Options |Array of [Option](https://docs.byteplus.com/en/docs/55/118245#option) |Refer to the Sample response. |List of available options for selector type parameters.<br><br>> **tip**<br><br><br>> This field is only supported by parameters of selector type (i.e., when `Type` is `radio`).<br> |
|ParamName |String |active\-defrag\-ignore\-bytes |Parameter name. |
|Range |String |[100,1024] |Value range for numeric parameters.<br><br>> **tip**<br><br><br>> Only some numeric type parameters (i.e., when `Type` is `number`) support this field.<br> |
|Type |String |number |Parameter type, with the following range of values:<br><br><br>* `radio`: Selector type.<br><br>* `number`: Numeric type.<br><br>* `string`: String type. |
|Unit |String |MB |Unit for numeric parameters.<br><br>> **tip**<br><br><br>> Only some numeric type parameters (i.e., when `Type` is `number`) support this field.<br> |

### Option

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Value |String |read_primary_node_only |Options for selector type parameters. |
|Description |String |Read requests are only sent to the primary node. |Description of optional parameters. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ApplyParameterGroup&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "ParameterGroupId": "pg-cnlfm5yzmxehmkw****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ApplyParameterGroup",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "ApplyParameterGroupInfo": {
            "InstanceId": "redis-cn0212gzmh2xs****",
            "ApplyParameters": [
                {
                    "CurrentValue": "60",
                    "Description": "在发布订阅客户端断开连接之前，输出缓冲区大小持续超过**client-output-buffer-pubsub-soft-limit**参数值的时间。单位：秒，取值范围1～900。",
                    "NeedReboot": false,
                    "Options": null,
                    "ParamName": "client-output-buffer-pubsub-soft-seconds",
                    "Range": "[1,900]",
                    "TargetValue": "1",
                    "Type": "number",
                    "Unit": "s"
                }
            ],
            "ParameterGroupId": "pg-cnlfm5yzmxehmkw****"
        }
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
