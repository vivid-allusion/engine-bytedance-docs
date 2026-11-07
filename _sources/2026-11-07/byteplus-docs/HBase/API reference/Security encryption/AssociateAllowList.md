---
title: "AssociateAllowList"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/AssociateAllowList"
---

Call the AssociateAllowList interface to associate the target instance with the specified allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["hb\-cnglda9068d1\*\*\*\*"] |ID of the instance to associate with an allowlist.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple instance IDs, separated by commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot pass multiple instance IDs and multiple allowlists ID at the same time. You can only associate multiple instances with one allowlist, or one instance with multiple allowlists.</div><br> |
|AllowListIds |Array of String |Yes |["acl\-1b7efcb4042b4744a8384dcafd1d\*\*\*\*"] |The ID of the allowlist to associate with the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple allowlist IDs, separated by commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot pass multiple instance IDs and multiple allowlists ID at the same time. You can only associate multiple instances with one allowlist, or one instance with multiple allowlists.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=AssociateAllowList&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceIds": [
        "hb-cnglda9068d1****"
    ],
    "AllowListIds": [
        "acl-1b7efcb4042b4744a8384dcafd1d****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20221113131915010174246136032B****",
        "Action": "AssociateAllowList",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
