---
title: "DescribeAllowListDetail"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail"
---

Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlist ID.<br><br>tip<br><br>You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query the information about all allowlists under the specified region, including allowlist IDs. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlist ID. |
|AllowListName |String |test |Name of allowlist. |
|AllowListDesc |String |test |Remarks about the allowlist. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Only IPv4 addresses are supported now. |
|AllowList |String |10.1. ** *.* ** ,10.2. ** *.* ** /24 |The list of IP addresses in the allowlist. |
|AssociatedInstances |Object[] | |Information about the instances that have been associated with the current allowlist. |
|VPC |String |vpc\-2743n1ihbxla87fap8tap\*\*\*\*\*\* |The VPC ID to which the instance belongs. |
|InstanceId |String |mongo\-replica\-e405f8e2\*\*\*\*\*\* |The instance IDs that have been associated with the current allowlist. |
|InstanceName |String |test |The instance names that have been associated with the current allowlist. |
|ProjectName |String |default |The project to which the instance belongs. |
|ProjectName |String |default |The project to which the current allowlist belongs. |
|AllowListCategory |String |Default |Allowlist type. The value range is as follows:<br><br><br>* `Ordinary`: Ordinary allowlist.<br><br>* `Default`: Default allowlist. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeAllowListDetail&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202203161507260102252431180088****",
        "Action": "DescribeAllowListDetail",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowList": "10.1.***.***,10.2.***.***/24",
        "AllowListDesc": "test",
        "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****",
        "AllowListName": "test",
        "AllowListType": "IPv4",
        "AssociatedInstances": [
            {
                "InstanceId": "mongo-replica-e405f8e2****",
                "InstanceName": "test",
                "ProjectName": "default",
                "VPC": "vpc-3tgjebmlgq4e8i4m****"
            }
        ],
        "ProjectName": "default",
        "AllowListCategory": "Default"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
