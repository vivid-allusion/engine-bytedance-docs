---
title: "ModifyParameterGroup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifyparametergroup"
---

Call the ModifyParameterGroup API to modify the parameter template information (such as parameter template name, description, and parameter values in the template).

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyParameterGroup&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ParameterGroupId |String |Yes |pg\-cnlfm5yzmxehmkwbzk3 |Parameter template ID.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) API to query the basic information of all parameter templates under the current account and Region, including the parameter template ID.<br><br><br>* > Only custom parameter templates (i.e., where `Source` is `User`) are editable, system parameter templates (i.e., where `Source` is `System`) cannot be edited. For more details, see [Editing parameter template](https://docs.byteplus.com/en/docs/redis/edit-parameter-template).<br> |
|Name |String |Yes |test_temp |Name of the parameter template.<br><br>> **tip**<br><br><br><br>* > If you do not need to modify the name of the original parameter template, simply enter its original name. You can call the [DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) API to query the basic information of all parameter templates under the current account and region, including parameter template names.<br><br><br>* > To modify the parameter template name, simply enter the new name. The name must meet the following requirements:<br><br><br>   * > It cannot start with a number or hyphen (\-).<br><br><br>   * > It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>   * > The length should be 2 to 64 characters.<br> |
|Description |String |No |test template |Remarks for the parameter template, with a maximum length of 200 characters.<br><br>> **tip**<br><br><br><br>* > If this parameter is not set, the parameter template's remarks will not be modified.<br><br><br>* > If an empty string is passed in (i.e., `"Description":""`), the parameter template's remarks will be cleared.<br> |
|ParamValues |Array of [ParamValue](https://docs.byteplus.com/en/docs/55/37303#paramvalue) |Yes |Refer to the Sample response. |A list of parameter information to be included in the modified parameter template.<br><br>> **tip**<br><br><br><br>* > Each parameter template must contain at least one parameter.<br><br><br>* > For more details on parameters supported by Redis, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).<br> |

### ParamValue

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |maxmemory\-policy |Parameter names to be included in the modified parameter template.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) interface to query the configurable parameter information supported by the target Redis instance, including parameter names, supported value ranges, and so on.<br> |
|Value |String |Yes |allkeys\-lru |The parameter value to be set for the parameter that needs modification.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) interface to query the configurable parameter information supported by the target Redis instance, including parameter names, supported value ranges, and so on.<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyParameterGroup&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ParameterGroupId": "pg-cnlfm5yzmxehmkwbzk3",
    "Name": "test_temp",
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
        "Action": "ModifyParameterGroup",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
