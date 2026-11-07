---
title: "SyncAllowList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/syncallowlist"
---

Call the SyncAllowList API to synchronize the IPs of security groups bound to the whitelist.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-7cc722a6fd794193b71948613758\*\*\*\* |The ID of the whitelist that needs to be synchronized. |
|DryRun |Boolean |No |false |Whether to preview changes to the security groups in the whitelist. Valid values:<br><br><br>* `true`: Preview only, no synchronization.<br><br>* `false`: No preview, synchronize directly.<br><br><br>tip<br><br>This parameter is required. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|ChangeObjects |Object[] |null |Information about changes to the security groups bound to the whitelist.<br><br>tip<br><br>When the request parameter `DryRun` is set to `false`, the value of this return parameter is `null`. |
|AddedIpList |String[] |null |The newly added IPs in the security group. If no IPs are added, the value is `null`. |
|BindMode |String |AssociateEcsIp |The mode of associating a security group. Valid values:<br><br><br>* `IngressDirectionIp`: Inbound IP.<br><br>* `AssociateEcsIp`: Associate ECSIP. |
|HasChanged |Boolean |false |Whether there are changes in the IP addresses within the security group. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|HasDeleted |Boolean |false |Whether any IP addresses have been removed from the security group. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|NewIpList |String[] |[ "0.0.0.0/0"<br><br>] |The collection of IPs in the security group after synchronization. |
|OldIpList |String[] |[ "0.0.0.0/0"<br><br>] |The collection of IPs in the security group before synchronization. |
|RemovedIpList |String[] |null |The removed IPs from the security group. If no IPs are removed, the value is `null`. |
|SecurityGroupId |String |sg\-2zecpzrl456v4610wgmq2\*\*\*\* |The ID of the security group. |
|SecurityGroupName |String |SecurityGroup_Test |The name of the security group. |

## Sample request

```json
POST /?Action=SyncAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListId": "acl-7cc722a6fd794193b71948613758****",
    "DryRun": false
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025030712131826F34509F381596F3CC0-c6c4ad",
        "Action": "SyncAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ChangeObjects": null
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
