---
title: "DisassociateAllowList"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DisassociateAllowList"
---

Call the DisassociateAllowList to disassociate the instance from the allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After an instance is disassociated from an allowlist, none of the devices in that allowlist can access the instance. Please ensure that the device IP that also requires access to the current instance is added to the other allowlists.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisassociateAllowList&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["vedbm\-ca12cbqv\*\*\*\*"] |ID of the instance to disassociate with an allowlist.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You cannot specify multiple instance IDs and multiple allowlist IDs in the same request. You can either disassociate a single allowlist from multiple instances or multiple allowlists from a single instance.</div><br> |
|AllowListIds |Array of String |Yes |["acl\-c2402ba601374808aeb19d06acc2\*\*\*\*"] |The ID of the allowlist to be disassociated from the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You cannot specify multiple instance IDs and multiple allowlist IDs in the same request. You can either disassociate a single allowlist from multiple instances or multiple allowlists from a single instance.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DisassociateAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceIds": [
        "vedbm-umpu6wlg****",
        "vedbm-255rdo3f****",
        "vedbm-53gh6dsh****"
    ],
    "AllowListIds": [
        "acl-0b4b2f1d2a0a40169a2835994459****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202203161718320102252431180280****",
        "Action": "DisassociateAllowList",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
