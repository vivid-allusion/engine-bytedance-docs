---
title: "DeleteDBInstance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deletedbinstance"
---

Call the DeleteDBInstance API to delete a specified Redis instance.

## Request type

Asynchronous request.

## Precautions

When you call the [DeleteDBInstance](https://docs.byteplus.com/en/docs/redis/deletedbinstance) API to delete an instance, the system automatically selects the corresponding default backup policy based on the instance type, including:

* Primary\-secondary instance: Before the instance is deleted, a final backup is created by default. We recommend that you download and save it locally in time. After deleting an instance, the instance data is **completely cleared** and cannot be retrieved. You can view and download backup of deleted instances on the **Backups** page. For more information, see [Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup).

* Single node instance: Single node instances do not support persistence and backup functions. No backup will be created by default when deleting, and instance data will be **completely cleared** after deletion. Please proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDBInstance&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|BackupPointName |String |No |testbackup |Set a backup name for the final backup of the instance to be deleted If no backup name is set, the backup ID is used as the name by default. <br><br>If you need to set a backup name, it must meet the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > This parameter only applies to **pay\-as\-you\-go** **primary\-secondary instances**, specifically instances where `InstanceClass` is `PrimarySecondary` and `ChargeType` is `PostPaid`.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specific instance, including its instance type and billing type.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteDBInstance&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"BackupPointName": "testbackup"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022012421383201022509900805A71111",
          "Action": "DeleteDBInstance",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
