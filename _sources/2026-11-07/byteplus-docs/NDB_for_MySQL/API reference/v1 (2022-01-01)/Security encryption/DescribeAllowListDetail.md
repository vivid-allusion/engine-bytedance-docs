---
title: "DescribeAllowListDetail"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowListDetail"
---

Call the DescribeAllowListDetail to query the detailed information of the allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAllowListDetail&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-b2a5bf3e471c433096232082c199\*\*\*\* |Allowlist ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowList |String |10.1.\*\*\*.\*\*\*,10.2.\*\*\*.\*\*\*/24 |The list of IP addresses in the allowlist. |
|AllowListDesc |String |test |The description of the allowlist. |
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlists ID. |
|AllowListName |String |test |Allowlist name. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Only `IPv4` is currently supported, representing an IPv4 address. |
|AssociatedInstanceNum |Long |0 |Number of associated instances. |
|ProjectName |String |default |The name of the project to which the allowlist belongs. |
|AssociatedInstances |Array of [AssociatedInstanceInfo](https://docs.byteplus.com/en/docs/265/57380#associatedinstanceinfo) |Refer to the return example. |Summary of instances associated with the current allowlist. |


<span id="associatedinstanceinfo"></span>
### AssociatedInstanceInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-ca12cbqv\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|VPC |String |vpc\-3tgjebmlgq4e8i4m\*\*\*\* |VPC ID。 |
|ProjectName |String |default |The name of the project to which the allowlist belongs. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeAllowListDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "AllowListId": "acl-04908986ad034ac0ba1fb1e3a754****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202203161507260102252431180088****",
        "Action": "DescribeAllowListDetail",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowList": "10.1.***.***,10.2.***.***/24",
        "AllowListDesc": "test",
        "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****",
        "AllowListName": "test",
        "AllowListType": "IPv4",
        "AssociatedInstanceNum": 1,
        "AssociatedInstances": [
            {
                "InstanceId": "vedbm-ca12cbqv****",
                "InstanceName": "test",
                "ProjectName": "default",
                "VPC": "vpc-3tgjebmlgq4e8i4m****"
            }
        ],
        "ProjectName": "default"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
