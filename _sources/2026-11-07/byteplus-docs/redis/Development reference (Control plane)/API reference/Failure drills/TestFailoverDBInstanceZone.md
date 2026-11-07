---
title: "TestFailoverDBInstanceZone"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/testfailoverdbinstancezone"
---

Call the TestFailoverDBInstanceZone API to simulate an availability zone\-level failover for the target Redis instance.

## Request type

Asynchronous request.

## Limits Only Redis Instances with multi\-availability zone deployed (that is, in the response of the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API, the `MultiAZ` returns `enabled` ) support calling this API. For more details, refer to [Deploying in multiple availability zones](https://docs.byteplus.com/en/docs/redis/deploy-multi-az).

## Precautions

* During the availability zone\-level failover process, the instance may have one to two temporary disconnections (each disconnection lasts up to 30 seconds). Please proceed with caution, and ensure that the client has the correct retry mechanism.

* The time required for zone\-level failover is affected by various factors (such as network environment, task queue, data volume, etc.), and it is recommended to perform the operation during off\-peak business hours.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TestFailoverDBInstanceZone&serviceCode=Redis&version=2020-12-07&groupName=故障演练)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii87hla |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|FailedZoneId |String |Yes |cn\-beijing\-a |Availability Zone ID for simulating a fault.<br><br>> **tip**<br><br><br>> You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query all availability zone information for Redis in the specified region, including the Availability Zone ID.<br> |
|FailbackToPrimaryDelayInMinutes |Long |No |5 |Failover duration before automatically switching back to the primary availability zone. Unit: minutes. Valid values:<br><br><br>* 5。<br><br>* 10。<br><br>* 15。<br><br><br>> **tip**<br><br><br><br>* > This parameter takes effect only when simulating a failover for the primary availability zone of the instance (i.e., the first availability zone returned by `ZoneIds` in the result of calling the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API).<br><br><br>* > If this parameter is left blank, it means there is no need to automatically switch back to the primary availability zone. After the failover is complete, the primary node may be located in the secondary availability zone, and the secondary node in the primary availability zone. After the failover is complete, you can call the [a](https://docs.byteplus.com/en/docs/redis/modifydbinstanceazconfigure)[a](https://docs.byteplus.com/en/docs/redis/modifydbinstanceazconfigure) API to manually switch the instance's availability zone.<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=TestFailoverDBInstanceZone&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cnlfkmh6uiii87hla",
    "FailedZoneId": "cn-beijing-a",
    "FailbackToPrimaryDelayInMinutes": 5
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TestFailoverDBInstanceZone",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
