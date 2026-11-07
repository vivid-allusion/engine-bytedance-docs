---
title: "DeleteAllowList"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DeleteAllowList"
---

Call the DeleteAllowList API to delete a specified allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

An Allowlist can be deleted only after all instances are disassociated from it. You can call the [DisassociateAllowList](https://docs.byteplus.com/en/docs/HBase/DisassociateAllowList) API to disassociate instances from an allowlist.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-c2402ba601374808aeb19d06acc2\*\*\*\* |Allowlist ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DeleteAllowList&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "AllowListId": "acl-c2402ba601374808aeb19d06acc2****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202204151506390101940591001265****",
        "Action": "DeleteAllowList",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
