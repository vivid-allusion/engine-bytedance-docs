---
title: "SyncAllowList"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/SyncAllowList"
---

Call the SyncAllowList API to synchronize the IP addresses of the security groups bound in the allowlist.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=SyncAllowList&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

Request parameter description

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |No |acl\-cn02zv7944lzokt\*\*\*\* |The ID of the allowlist to be synchronized. |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/55/118242#securitygroupbindinfo) |No |Refer to the sample request. |After a security group is passed in, the system will check whether the IP address bound to the specified security group has changed. |
|DryRun |Boolean |No |false |Specifies whether to preview changes to the security group in the allowlists. Values: <br><br><br>* `true`: Preview only, do not synchronize. Default value.<br><br>* `false`: skips the preview and synchronizes directly. |

### SecurityGroupBindInfo

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|BindMode |String |Yes |AssociateEcsIp |Security group association mode. Valid values:<br><br><br>* `IngressDirectionIp`: Inbound IP, which allows IP addresses involved in TCP and ALL protocols in the inbound source addresses of the security groups to access the database. If the source address is configured as a security group, it will be ignored.<br><br>* `AssociateEcsIp`: Associate ECS IP. This allows Elastic Compute Service instances within the security groups to access the database. Currently, only IP information from the primary network interface is supported for import.<br><br><br>> **tip**<br><br><br>> For more details on the security group association mode, see [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).<br> |
|SecurityGroupId |String |Yes |sg\-rrzrivu0yc5cv0x588n\*\*\*\* |The security group ID to associate.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query security group information, including the security group ID.<br><br><br>* > Up to 10 security groups can be added to a single allowlist at a time.<br><br><br>* > An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br> |

## Response parameters

Response parameter description

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ChangeObjects |Array of [SyncSecurityGroupChangeObject](https://docs.byteplus.com/en/docs/55/118242#syncsecuritygroupchangeobject) |Refer to the Sample response. |Change information of the security group associated with the allowlist. When the value of the request parameter DryRun is `false`, the value of this returned parameter is`null`。 |

### SyncSecurityGroupChangeObject

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AddedIpList |Array of String |["192.168.0.100"] |New IP set. |
|BindMode |String |AssociateEcsIp |Security group association mode. |
|HasChanged |Boolean |true |Indicates whether the IP addresses in this security group have changed. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|HasDeleted |Boolean |false |Indicates whether an IP address is removed from the security group. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|NewIpList |Array of String |["192.168.0.1,192.168.0.100"] |IP address allowlist after security group synchronization. |
|OldIpList |Array of String |["192.168.0.1"] |IP address allowlist before security group synchronization. |
|RemovedIpList |Array of String |[""] |List of IP addresses removed during security group synchronization. |
|SecurityGroupId |String |sg\-rrzrivu0yc5cv0x588n\*\*\*\* |Security group ID. |
|SecurityGroupName |String |test sg |Security group name. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=SyncAllowList&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "AllowListId": "acl-cn02zv7944lzokt****",
    "DryRun": false
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SyncAllowList",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChangeObjects": [
            {
                "AddedIpList": null,
                "BindMode": "AssociateEcsIp",
                "HasChanged": true,
                "HasDeleted": false,
                "NewIpList": [],
                "OldIpList": [
                    "192.168.0.5",
                    "192.168.0.9"
                ],
                "RemovedIpList": [
                    "192.168.0.5",
                    "192.168.0.9"
                ],
                "SecurityGroupId": "sg-3jh6o7p9o6xa83pncmfva****",
                "SecurityGroupName": "SG-test"
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
