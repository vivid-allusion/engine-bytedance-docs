---
title: "DeleteParameterGroup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deleteparametergroup"
---

Call the DeleteParameterGroup API to delete the target parameter template.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteParameterGroup&serviceCode=Redis&version=2020-12-07&groupName=参数管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ParameterGroupId |String |Yes |pg\-cnlfm5yzmxehmkwbzk3 |Parameter template ID.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) API to query the basic information of all parameter templates under the current account and Region, including the parameter template ID.<br><br><br>* > Only custom parameter templates (where `Source` is `User`) can be deleted; system parameter templates (where `Source` is `System`) cannot be deleted.<br><br><br>* > The template cannot be recovered after deletion. Proceed with caution. For more details, refer to [Deleting a parameter template](https://docs.byteplus.com/en/docs/redis/delete-parameter-template).<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteParameterGroup&Version=2020-12-07 HTTP/1.1
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
        "RequestId": "20230604110420100232280022D31",
        "Action": "DeleteParameterGroup",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
