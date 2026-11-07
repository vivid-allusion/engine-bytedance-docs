---
title: "DescribeAllowListDetail"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeAllowListDetail"
---

Call the DescribeAllowListDetail API to view the details of a specified allowlist, including its IP addresses and associate instances.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-4a8ade08756c4433801a91e3a2ee\*\*\*\* |Allowlist ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|AllowList |String |10.1. ** *.* ** ,10.2. ** *.* ** /24 |The list of IP addresses in the allowlist. |
|AllowListDesc |String |test |The description of the allowlist. |
|AllowListId |String |acl\-4a8ade08756c4433801a91e3a2ee\*\*\*\* |Allowlists ID. |
|AllowListName |String |test |Allowlist name. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Only IPv4 addresses are currently supported. |
|AssociatedInstances |Array of [AssociatedInstanceInfo](https://docs.byteplus.com/en/docs/219/60869#associatedinstanceinfo) |Refer to the Sample response. |Summary of instances associated with the current allowlist. |
|AssociatedInstanceNum |Long |5 |The number of instances associated with the allowlist. |
|AllowListCategory |String |Ordinary |Allowlist category. Value:<br><br><br>* `Ordinary`: An ordinary allowlist.<br><br>* `Default`: A default allowlist. |


<span id="associatedinstanceinfo"></span>
### AssociatedInstanceInfo


|Name |Type |Example value |Description |
|---|---|---|---|
|InstanceId |String |hb\-cnglb4b26770\*\*\*\* |The ID of the instance associated with the current allowlist. |
|InstanceName |String |test |The names of instances associated with the current allowlist. |
|VPC |String |vpc\-2743n1ihbxla87fap8tap\*\*\*\* |The private network ID of the instance. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DescribeAllowListDetail&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "AllowListId": "acl-4a8ade08756c4433801a91e3a2ee****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022111021572201017424420901C4****",
        "Action": "DescribeAllowListDetail",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowList": "100.0.0.1",
        "AllowListCategory": "Ordinary",
        "AllowListDesc": "test_list",
        "AllowListId": "acl-4a8ade08756c4433801a91e3a2ee****",
        "AllowListName": "test",
        "AllowListType": "IPv4",
        "AssociatedInstanceNum": 1,
        "AssociatedInstances": [
            {
                "InstanceId": "hb-cnglb4b26770****",
                "InstanceName": "test-api",
                "VPC": "vpc-3ret6bva9k54w5zsk2iku****"
            }
        ]
    }
}
```
