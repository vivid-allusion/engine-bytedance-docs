---
title: "DescribeParameterGroupDetail"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeparametergroupdetail"
---

Call the DescribeParameterGroupDetail API to query details about the target parameter template.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeParameterGroupDetail&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ParameterGroupId |String |Yes |pg\-cnlfm5yzmxehmkwbzk3 |Parameter templates ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) API to query the basic information of all parameter templates under the current account and Region, including the parameter template ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterGroupInfo |Object of [ParameterGroupInfo](https://docs.byteplus.com/en/docs/55/37305#parametergroupinfo) |Refer to the Sample response. |Parameter template details. |

### ParameterGroupInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |test_temp |Name of the parameter template. |
|Source |String |User |Creation source of the parameter template, the value range is as follows:<br><br><br>* `User`: User created (i.e., custom template).<br><br>* `System`: System created (i.e., system template). |
|Default |Boolean |false |Whether it is the default parameter template.<br><br>> **tip**<br><br><br>> For Cache for Redis, a default system parameter template is created for each database version. The template contains all the parameters supported by this version and the default parameter values. For more details, see [Parameter template management](https://docs.byteplus.com/en/docs/redis/parameter-template-overview).<br> |
|CreateTime |String |2025\-01\-09T02:51:23Z |Creation time of the parameter template, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|Parameters |Array of [ParameterInfo](https://docs.byteplus.com/en/docs/55/37305#parameterinfo) | |List of parameter information included in the parameter template. |
|UpdateTime |String |2025\-01\-09T03:10:11Z |The last update time of the parameter template, in `yyyy-MM-ddTHH:mm:ssZ` (UTC) format. |
|Description |String |test template |Description of the parameter template. |
|EngineVersion |String |7.0 |The database version to which the parameter template applies. |
|ParameterGroupId |String |pg\-cnlfm5yzmxehmkwbzk3 |Parameter templates ID. |

### ParameterInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CurrentValue |String |100 |The running value of this parameter in the parameter template. |
|Description |String |Minimum fragmented space to trigger memory defragmentation. Unit: MB, value range 100–1024. |Parameter description. |
|NeedReboot |Boolean |false |Whether an instance restart is required for the modification to take effect. Valid values:<br><br><br>* `true`: requires restart.<br><br>* `false`: No restart required. |
|Options |Array of [Option](https://docs.byteplus.com/en/docs/55/37305#option) |Refer to the Sample response. |List of available options for selector type parameters.<br><br>> **tip**<br><br><br>> This field is only supported by parameters of selector type (i.e., when `Type` is `radio`).<br> |
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
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeParameterGroupDetail&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ParameterGroupId": "pg-cnlfm5yzmxehmkwbzk3"
}
```

## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250109111105F5EFEE526915BC478790-b8aa7f",
    "Action": "DescribeParameterGroupDetail",
    "Version": "2020-12-07",
    "Service": "Redis",
    "Region": "cn-beijing"
  },
  "Result": {
    "ParameterGroupInfo": {
      "CreateTime": "2025-01-09T02:51:23Z",
      "Default": false,
      "Description": "test template",
      "EngineVersion": "7.0",
      "Name": "test_temp",
      "ParameterGroupId": "pg-cnlfm5yzmxehmkwbzk3",
      "Parameters": [
        {
          "CurrentValue": "100",
          "Description": "触发内存碎片整理，碎片空间占用量的最小值。单位：MB，取值范围100～1024。",
          "NeedReboot": false,
          "Options": null,
          "ParamName": "active-defrag-ignore-bytes",
          "Range": "[100,1024]",
          "Type": "number",
          "Unit": "MB"
        }
      ],
      "Source": "User",
      "UpdateTime": "2025-01-09T03:10:11Z"
    }
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
