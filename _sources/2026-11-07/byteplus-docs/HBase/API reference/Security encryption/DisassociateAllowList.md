---
title: "DisassociateAllowList"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DisassociateAllowList"
---

Call the DisassociateAllowList interface to disassociate the target instance from the specified allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After disassociating an instance from an allowlist, all devices in that allowlist can no longer access the instance. Ensure that the IP addresses of devices that still need to access the current instance are added to other allowlists.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["hb\-cnglda9068d1\*\*\*\*"] |ID of the instance to disassociate with an allowlist.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple instance IDs, separated by commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot specify multiple instance IDs and multiple allowlist IDs in the same request. You can only disassociate multiple instances from a single allowlist or one instance from multiple allowlists at a time.</div><br> |
|AllowListIds |Array of String |Yes |["acl\-c2402ba601374808aeb19d06acc2\*\*\*\*"] |The ID of the allowlist to be disassociated from the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple allowlist IDs, separated by commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot specify multiple instance IDs and multiple allowlist IDs in the same request. You can only disassociate multiple instances from a single allowlist or one instance from multiple allowlists at a time.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DisassociateAllowList&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "AllowListIds": [
        "acl-c2402ba601374808aeb19d06acc2****"
    ],
    "InstanceIds": [
        "hb-cnglda9068d1****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022111313270101017424912601D7****",
        "Action": "DisassociateAllowList",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
