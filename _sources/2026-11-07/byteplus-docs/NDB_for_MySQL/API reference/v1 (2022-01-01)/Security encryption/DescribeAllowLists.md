---
title: "DescribeAllowLists"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists"
---

Call the DescribeAllowLists to query all allowlist information in the specified area under the current account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAllowLists&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRegions">DescribeRegions</a> API to query information about regions where instances can be created, including the region ID.</div><br> |
|InstanceId |String |No |vedbm\-ca12cbqv\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br> |
|ProjectName |String |No |default |The name of the project to which the allowlist belongs. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowLists |Array of [AllowListInfo](https://docs.byteplus.com/en/docs/265/57378#allowlistinfo) |Refer to the Sample response. |The list of allowlist information. |


<span id="allowlistinfo"></span>
### AllowListInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-31f52387922a40a7a60ff21365f6\*\*\*\* |Allowlist ID |
|AllowListName |String |byte\*\*\*\* |Allowlist name. |
|AllowListDesc |String |test |The description of the allowlist. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Only `IPv4` is currently supported, representing an IPv4 address. |
|AllowListIPNum |Long |3 |The total number of IPs or IP segments. |
|AssociatedInstanceNum |Long |0 |The number of instances associated with the allowlist. |
|ProjectName |String |default |The name of the project to which the allowlist belongs. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeAllowLists&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "RegionId": "cn-beijing",
    "InstanceId": "vedbm-ca12cbqv****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20220316143231010225099008069A****",
        "Action": "DescribeAllowLists",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowLists": [
            {
                "AllowListDesc": "test",
                "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****",
                "AllowListName": "test",
                "AllowListIPNum": 2,
                "AllowListType": "IPv4",
                "AssociatedInstanceNum": 1,
                "ProjectName": "default"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
