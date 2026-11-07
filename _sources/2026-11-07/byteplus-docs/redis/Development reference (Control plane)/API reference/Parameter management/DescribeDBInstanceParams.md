---
title: "DescribeDBInstanceParams"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstanceparams"
---

Call the DescribeDBInstanceParams API to query the list of parameters supported by the target Redis instance.

## Request type

Synchronous request.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceParams&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|PageNumber |Integer |Yes |1 |The page number for the parameter information list. Its value does not exceed the maximum value of the Integer data type, and it starts from 1. |
|PageSize |Integer |Yes |1 |Number of records per page. An integer with a value between 1 and 1000. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Params |Array of [InstanceParamInfo](https://docs.byteplus.com/en/docs/55/12473#instanceparaminfo) |Refer to the sample response. |Parameter information list.<br><br>> **tip**<br><br><br>> For more information on parameters supported by Redis instances, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).<br> |
|TotalParamsNum |Integer |33 |Total count of parameter information list. |

### InstanceParamInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParamName |String |active\-defrag\-ignore\-bytes |Parameter name. |
|Type |String |number |Parameter type, with the following range of values:<br><br><br>* `radio`: Selector type.<br><br>* `number`: Numeric type.<br><br>* `string`: String type. |
|Unit |String |MB |Unit for numeric parameters.<br><br>> **tip**<br><br><br>> Only some numeric type parameters (i.e., when `Type` is `number`) support this field.<br> |
|Range |String |[100,1024] |Value range for numeric parameters.<br><br>> **tip**<br><br><br>> Only some numeric type parameters (i.e., when `Type` is `number`) support this field.<br> |
|Options |Array of [Option](https://docs.byteplus.com/en/docs/55/12473#option) |Refer to the Sample response. |List of available options for selector type parameters.<br><br>> **tip**<br><br><br>> This field is only supported by parameters of selector type (i.e., when `Type` is `radio`).<br> |
|NeedReboot |Boolean |true |Whether an instance restart is required for the modification to take effect. Valid values:<br><br><br>* `true`: requires restart.<br><br>* `false`: No restart required. |
|Description |String |Maximum CPU percentage for memory defragmentation. The value ranges from 1 to 40. |Parameter description. |
|CurrentValue |String |100 |Current running value of the parameter. |
|DefaultValue |String |100 |Parameter default value. |
|EditableForInstance |Boolean |true |Whether the current instance supports editing this parameter. Valid values:<br><br><br>* `true`: Supported.<br><br>* `false`: Not supported. |

### Option

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Value |String |read_primary_node_only |Options for selector type parameters. |
|Description |String |Read requests are only sent to the primary node. |Description of optional parameters. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceParams&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs****",
	"PageNumber": 1,
	"PageSize": 1
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024071619492773617F0DF933C71F28F2-d1f478",
        "Action": "DescribeDBInstanceParams",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-shanghai"
    },
    "Result": {
        "Params": [
            {
                "CurrentValue": "25",
                "DefaultValue": "25",
                "Description": "内存碎片整理占用的最大CPU百分比。取值范围1～40。",
                "EditableForInstance": true,
                "NeedReboot": false,
                "Options": null,
                "ParamName": "active-defrag-cycle-max",
                "Range": "[1,40]",
                "Type": "number",
                "Unit": ""
            }
        ],
        "TotalParamsNum": 33
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
