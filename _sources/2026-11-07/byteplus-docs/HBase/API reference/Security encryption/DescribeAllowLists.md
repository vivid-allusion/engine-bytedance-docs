---
title: "DescribeAllowLists"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists"
---

Call the DescribeAllowLists API to query all IP allowlists in a specified region for the current account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeRegions">DescribeRegions</a> API to query resource information in all available regions for the instance, including the Region ID.</div><br> |
|InstanceId |String |No |hb\-cnglbbb73ea0\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|AllowLists |Array of [AllowListInfo](https://docs.byteplus.com/en/docs/219/60868#allowlistinfo) |Refer to the Sample response. |The list of allowlist information. |


<span id="allowlistinfo"></span>
### AllowListInfo


|Name |Type |Example value |Description |
|---|---|---|---|
|AllowListDesc |String |test |The description of the allowlist. |
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlist ID |
|AllowListName |String |test |Allowlist name. |
|AllowListIPNum |Long |2 |The total number of IP addresses or address blocks in the allowlist. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Only IPv4 addresses are currently supported. |
|AssociatedInstanceNum |Long |1 |The total number of instances associated with the allowlist. |
|AllowListCategory |String |Ordinary |Allowlist category. Value:<br><br><br>* `Ordinary`: An ordinary allowlist.<br><br>* `Default`: A default allowlist. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DescribeAllowLists&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "RegionId": "cn-beijing",
    "InstanceId": "hb-cnglbbb73ea0****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202211102158400101742461360830****",
        "Action": "DescribeAllowLists",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowLists": [
            {
                "AllowListCategory": "Default",
                "AllowListDesc": "",
                "AllowListIPNum": 2,
                "AllowListId": "acl-4a8ade08756c4433801a91e3a2ee****",
                "AllowListName": "test",
                "AllowListType": "IPv4",
                "AssociatedInstanceNum": 2
            }
        ]
    }
}
```
