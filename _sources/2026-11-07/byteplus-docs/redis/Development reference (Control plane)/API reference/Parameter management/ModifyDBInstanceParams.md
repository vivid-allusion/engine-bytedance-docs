---
title: "ModifyDBInstanceParams"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams"
---

Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance.

## Request type

Asynchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceParams&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ParamValues |Array of [ParamValue](https://docs.byteplus.com/en/docs/55/12472#paramvalue) |Yes |Refer to the sample request. |Information about the parameter configuration items to be modified.<br><br>> **tip**<br><br><br>> For more information on parameters supported by Redis instances, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### ParamValue

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Name |String |No |maxmemory\-policy |Name of the parameter to modify.<br><br>> **tip**<br><br><br><br>* > If this field is left empty, no parameters will be modified by default (meaning `"Name": ""` will be passed by default).<br><br><br>* > You can call the [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) interface to query the configurable parameter information supported by the target Redis instance, including parameter names, supported value ranges, and so on.<br> |
|Value |String |No |allkeys\-lru |The parameter value of the parameter to modify.<br><br>> **tip**<br><br><br><br>* > If this field is left blank, no parameter value will be set for the target parameter by default (i.e., `\"Value\": \"\"` will be passed).<br><br><br>* > You can call the [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) interface to query the configurable parameter information supported by the target Redis instance, including parameter names, supported value ranges, and so on.<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceParams&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"ParamValues": [{
		"Name": "maxmemory-policy",
		"Value": "allkeys-lru"
	}]
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041518471701021216203114631111",
          "Action": "ModifyDBInstanceParams",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
