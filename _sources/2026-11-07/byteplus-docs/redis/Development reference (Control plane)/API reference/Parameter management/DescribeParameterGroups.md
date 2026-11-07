---
title: "DescribeParameterGroups"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeparametergroups"
---

Call the DescribeParameterGroups API to query basic information about parameter templates under the current account and region.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeParameterGroups&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|EngineVersion |String |No |7.0 |Redis database version applicable to the parameter template. The value range is as follows:<br><br><br>* `7.0`: Redis 7.0.<br><br>* `6.0`: Redis 6.0.<br><br>* `5.0`: Redis 5.0.<br><br><br>> **tip**<br><br><br>> If this parameter is left blank, it means that the database version number condition of the parameter template is not used for filtering.<br> |
|Source |String |No |User |Creation source of the parameter template, the value range is as follows:<br><br><br>* `User`: User created (i.e., custom template).<br><br>* `System`: System created (i.e., system template).<br><br><br>> **tip**<br><br><br>> If this parameter is left blank, it means that the creation source condition of the parameter template is not used for filtering.<br> |
|PageNumber |Integer |Yes |1 |Page number of the parameter template information list. The value does not exceed the maximum value of the Integer data type, and all starting values are 1. |
|PageSize |Integer |Yes |10 |Number of records per page. An integer from 1 to 100. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterGroups |Array of [ParameterGroupInfo](https://docs.byteplus.com/en/docs/55/37304#parametergroupinfo) |Refer to the Sample response. |Parameter template information list. |
|Total |Integer |1 |Total number of parameter templates. |

### ParameterGroupInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |test_temp |Name of the parameter template. |
|Source |String |User |Creation source of the parameter template, the value range is as follows:<br><br><br>* `User`: User created (i.e., custom template).<br><br>* `System`: System created (i.e., system template). |
|Default |Boolean |false |Whether it is the default parameter template.<br><br>> **tip**<br><br><br>> For Cache for Redis, a default system parameter template is created for each database version. The template contains all the parameters supported by this version and the default parameter values. For more details, see [Parameter template management](https://docs.byteplus.com/en/docs/redis/parameter-template-overview).<br> |
|CreateTime |String |2025\-01\-09T02:51:23Z |Creation time of the parameter template, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|UpdateTime |String |2025\-01\-09T03:10:11Z |The last update time of the parameter template, in `yyyy-MM-ddTHH:mm:ssZ` (UTC) format. |
|Description |String |test template |Description of the parameter template. |
|ParameterNum |Integer |2 |Number of parameters in the parameter template. |
|EngineVersion |String |7.0 |The database version to which the parameter template applies. |
|ParameterGroupId |String |pg\-cnlfm5yzmxehmkwbzk3 |Parameter templates ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeParameterGroups&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "EngineVersion": "7.0",
    "Source": "User",
    "PageNumber": 1,
    "PageSize": 10
}
```

## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250109105318A40F83EE441D5D4985B1-d228ce",
    "Action": "DescribeParameterGroups",
    "Version": "2020-12-07",
    "Service": "Redis",
    "Region": "cn-beijing"
  },
  "Result": {
    "ParameterGroups": [
      {
        "CreateTime": "2025-01-09T02:51:23Z",
        "Default": false,
        "Description": "test template",
        "EngineVersion": "7.0",
        "Name": "test_temp",
        "ParameterGroupId": "pg-cnlfm5yzmxehmkwbzk3",
        "ParameterNum": 13,
        "Source": "User",
        "UpdateTime": "2025-01-09T02:51:23Z"
      }
    ],
    "Total": 1
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
