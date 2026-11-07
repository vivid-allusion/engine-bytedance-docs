---
title: "ModifyAllowList"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/ModifyAllowList"
---

Call the ModifyAllowList API to modify the information of a specified allowlist, such as its name and IP addresses.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|AllowListId |String |No |acl\-04908986ad034ac0ba1fb1e3a754\*\*\*\* |Allowlist ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br> |
|AllowListName |String |No |test |Allowlist name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To modify the IP addresses in an allowlist, enter the name of the allowlist. You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query information about all allowlists in a specified Region, including allowlist names.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To rename an allowlist, enter the new name. The naming convention is as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Cannot start with digits or hyphen (\-).</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The length is 1~32 characters.</div><br> |
|ModifyMode |String |No |Cover |Modification methods are as follows:<br><br><br>* `Cover` (Default value): Overwrites the original allowlist with the value of the `AllowList` parameter.<br><br>* `Append`: Adds the Internet protocol addresses in the `AllowList` parameter to the original allowlist.<br><br>* `Delete`: Deletes the Internet protocol addresses in the `AllowList` parameter from the original allowlist. At least one IP address must be retained. |
|AllowListDesc |String |No |test |The description of the allowlist cannot exceed 200 characters. |
|AllowList |String |No |192.168.0.1 |Enter an IP address or an IP address range in CIDR format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist supports a maximum of 300 IP addresses or IP address segments in CIDR format. Duplicate addresses are not allowed. Separate multiple addresses with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set <code>127.0.0.1</code> to disable all address access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting CIDR <code>192.168.1.0/24</code> means that IP addresses within this network segment are allowed to access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set to <code>192.168.1.1</code> to allow access from this IP address only.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disable settings <code>0.0.0.0/0</code>.</div><br> |
|ApplyInstanceNum |Long |No |1 |The number of instances associated with the current allowlist.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when modifying the <code>AllowList</code> parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is used to confirm the scope of this modification to prevent failures caused by incorrect operations. You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists">DescribeAllowLists</a> API to query information about all allowlists in a specified region, including the total number of associated instances.</div><br> |
|AllowListCategory |String |No |Ordinary |Allowlist category. Value:<br><br><br>* `Ordinary`: An ordinary allowlist.<br><br>* `Default`: The default allowlist.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting a new default allowlist automatically replaces the previous one. The previous default allowlist becomes a regular allowlist.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=ModifyAllowList&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "AllowListId": "acl-04908986ad034ac0ba1fb1e3a754****",
    "AllowListName": "test",
    "AllowListDesc": "test",
    "AllowList": "192.168.0.1",
    "ModifyMode": "Cover",
    "ApplyInstanceNum": 1,
    "AllowListCategory": ""
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202211131252200101742442020852****",
        "Action": "ModifyAllowList",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
