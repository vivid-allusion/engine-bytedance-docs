---
title: "CreateParameterGroup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createparametergroup"
---

Call the CreateParameterGroup API to create a parameter template.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateParameterGroup&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |test_temp |Name of the parameter template. The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
|EngineVersion |String |Yes |7.0 |Redis database version supported by the parameter template. Valid values:<br><br><br>* `7.0`: Redis 7.0.<br><br>* `6.0`: Redis 6.0.<br><br>* `5.0`: Redis 5.0. |
|Description |String |No |test template |Remarks for the parameter template, with a maximum length of 200 characters.<br><br>> **tip**<br><br><br>> If this parameter is not set, the remark of the new parameter template will be empty by default.<br> |
|ParamValues |Array of [ParamValue](https://docs.byteplus.com/en/docs/55/37302#paramvalue) |Yes |Refer to the sample request. |List of parameter information to be included in the new parameter template.<br><br>> **tip**<br><br><br><br>* > Each parameter template must contain at least one parameter.<br><br><br>* > For more details on parameters supported by Redis, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).<br> |

### ParamValue

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |maxmemory\-policy |The parameter names to be included in the parameter template.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) interface to query the configurable parameter information supported by the target Redis instance, including parameter names, supported value ranges, and so on.<br> |
|Value |String |Yes |allkeys\-lru |The parameter value set for the corresponding parameter.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) interface to query the configurable parameter information supported by the target Redis instance, including parameter names, supported value ranges, and so on.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterGroupId |String |pg\-cnlfm5yzmxehmkwbzk3 |Parameter templates ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateParameterGroup&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "Name": "test_temp",
    "EngineVersion": "7.0",
    "Description": "test template",
    "ParamValues": [
        {
            "Name": "maxmemory-policy",
            "Value": "allkeys-lru"
        }
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31",
        "Action": "CreateParameterGroup",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "ParameterGroupId": "pg-cnlfm5yzmxehmkwbzk3"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
