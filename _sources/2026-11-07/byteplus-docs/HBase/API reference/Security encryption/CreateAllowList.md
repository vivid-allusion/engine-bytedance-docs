---
title: "CreateAllowList"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/CreateAllowList"
---

Call the CreateAllowList interface to create a new allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|AllowListName |String |Yes |test |The allowlist name must meet the following requirements:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~32 characters.<br><br>* The name cannot be the same as an existing allowlist name. |
|AllowListDesc |String |No |test |The description of the allowlist cannot exceed 200 characters. |
|AllowListType |String |No |IPv4 |The type of IP addresses in the allowlist. Only IPv4 addresses are currently supported, with a default value of `IPv4`. |
|AllowList |String |Yes |10.1.1.1,10.2.3.0/24 |Enter an IP address or an IP address range in CIDR format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist can contain a maximum of 300 IP addresses or IP address segments. Duplicate addresses are not allowed. Separate multiple addresses with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set <code>127.0.0.1</code> to disable all address access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting CIDR <code>192.168.1.0/24</code> means that IP addresses within this network segment are allowed to access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set to <code>192.168.1.1</code> to allow access from this IP address only.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disable settings <code>0.0.0.0/0</code>.</div><br> |
|AllowListCategory |String |No |Ordinary |Allowlist category. Value:<br><br><br>* `Ordinary`: An ordinary allowlist (default).<br><br>* `Default`: The default allowlist.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting a new default allowlist automatically replaces the previous one. The previous default allowlist becomes a regular allowlist.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|AllowListId |String |acl\-e32bde5839254d4bbc10601656ca\*\*\*\* |Allowlist ID |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=CreateAllowList&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "AllowListName": "test",
    "AllowList": "10.1.1.1,10.2.3.0/24"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202204151506390101940591001265****",
        "Action": "CreateAllowList",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowListId": "acl-e32bde5839254d4bbc10601656ca****"
    }
}
```
