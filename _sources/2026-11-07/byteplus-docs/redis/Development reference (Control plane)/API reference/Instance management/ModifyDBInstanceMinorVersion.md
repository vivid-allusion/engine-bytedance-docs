---
title: "ModifyDBInstanceMinorVersion"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceminorversion"
---

Call the ModifyDBInstanceMinorVersion API to upgrade target Redis instance to specified minor version.

## Request type

Asynchronous request.

## Precautions

* After initiating a minor version upgrade, the system first prepares node resources for the corresponding version. During switching, the database may experience brief disconnections (1~3 times) or enter read\-only status for seconds. Operate with caution. For more details, refer to [Upgrading minor version](https://docs.byteplus.com/en/docs/redis/upgrade-minor-version).

* It is recommended to perform the switch operation during off\-peak business hours and ensure the application has an automatic reconnection mechanism to minimize the impact of the operation on your business.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceMinorVersion&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii87hla |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|SwitchoverImmediately |Boolean |Yes |true |Whether to execute the switchover immediately. Valid values:<br><br><br>* `true`: Switch immediately.<br><br>* `false`: Switch during maintenance period.<br><br><br>> **tip**<br><br><br>> After initiating a minor version upgrade, the system first prepares node resources for the corresponding version. For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|ServerVersion |String |No |7.602.0 |The target server version for upgrade.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the current server version of instance will not be modified by default.<br><br><br>* > `ServerVersion` and `ProxyVersion` cannot be empty simultaneously.<br><br><br>* > You can call the [DescribeDBEngineVersions](https://docs.byteplus.com/en/docs/redis/describedbengineversions) API to query list of minor versions supported by Redis major versions, including information on each server version number. For more details about server versions, refer to [Server version release log](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log?lang=en#J0CFZO9x).<br> |
|ProxyVersion |String |No |1.602.0 |The target proxy version for upgrade.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the instance's current Proxy version will not be modified by default.<br><br><br>* > `ServerVersion` and `ProxyVersion` cannot be empty simultaneously.<br><br><br>* > You can call the [DescribeDBEngineVersions](https://docs.byteplus.com/en/docs/redis/describedbengineversions) API to query list of minor versions supported by Redis major versions, including information on each proxy version number. For more details about proxy versions, refer to [Proxy version release log](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log?lang=en#.cHJveHkt54mI5pys5Y-R5biD5pel5b-X).<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBEngineVersion |Object of [DBEngineVersion](https://docs.byteplus.com/en/docs/55/91374#dbengineversion) |Refer to the Sample response. |Database version list. |

### DBEngineVersion

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Engine |String |Redis |Database engine. |
|EngineVersion |String |7.0 |Database engine version. |
|ServerVersion |Object of [VersionInfo](https://docs.byteplus.com/en/docs/55/91374#versioninfo) | |Current server version information of the instance. |
|ProxyVersion |Object of [VersionInfo](https://docs.byteplus.com/en/docs/55/91374#versioninfo) | |Current proxy version number of the instance. |

### VersionInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Version |String |7.512.0 |Current server version of the instance. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceMinorVersion&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cnlfkmh6uiii8****",
    "SwitchoverImmediately": true,
    "ServerVersion": "7.602.0",
    "ProxyVersion": "1.602.0"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420322810023228002****",
        "Action": "ModifyDBInstanceMinorVersion",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBEngineVersion": {
            "Engine": "Redis",
            "EngineVersion": "7.0",
            "ProxyVersion": {
                "Version": "1.512.0"
            },
            "ServerVersion": {
                "Version": "7.512.0"
            }
        }
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
