---
title: "ModifyAllowList"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyAllowList"
---

Call the ModifyAllowList to modify the allowlist information.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyAllowList&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-04908986ad034ac0ba1fb1e3a754\*\*\*\* |Allowlist ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists">DescribeAllowLists</a> API to query all allowlists in a specified region, including allowlist IDs.</div><br> |
|AllowListName |String |Yes |test |Allowlist name.<br><br><br>* To modify the allowlist name, set this parameter to the new allowlist name. The name must meet the following requirements:<br><br>   * Cannot start with digits or hyphen (\-).<br><br>   * It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>   * The length must be between 1 and 128 characters.<br><br>* If you do not need to modify the allowlist name, set this parameter to the original allowlist name. You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists) API to query information about all allowlists in a specified Region, including allowlist names. |
|ApplyInstanceNum |Long |No |1 |The number of instances associated with the allowlist.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter confirms the scope of the modification to prevent failures from operational errors.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when the AllowList parameter is specified. The parameter value is the total number of instances associated with the allowlist. You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists">DescribeAllowLists</a> API to query the total number of instances associated with an allowlist in a specified region.</div><br> |
|AllowList |String |No |192.168.1.0 |Enter an IP address or an IP address segment in CIDR format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when modifying the IP addresses in the allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when the ApplyInstanceNum parameter is specified.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Each allowlist supports up to 1,000 IP addresses or IP address ranges in CIDR format. Duplicate addresses are not allowed. Separate multiple addresses with commas (,). The following are special examples:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Setting 0.0.0.0/0 allows access from all addresses.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Setting 127.0.0.1 blocks access from all addresses.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Setting both 0.0.0.0/0 and 127.0.0.1 allows access from all addresses.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Setting CIDR 192.168.1.0/24 allows access from IP addresses within that network segment.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Setting 192.168.1.1 allows access from this IP address only.</div><br> |
|ModifyMode |String |No |Cover |The method for modifying the allowlist can be set to:<br><br><br>* `Cover` (Default value): Overwrites the original allowlist with the value of the AllowList parameter.<br><br>* `Append`: Adds the Internet protocol addresses in the AllowList parameter to the original allowlist.<br><br>* `Delete`: Deletes the Internet protocol addresses in the AllowList parameter from the original allowlist. At least one IP address must be retained. |
|AllowListDesc |String |No |test |The description of the allowlist cannot exceed 200 characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "AllowListId": "acl-04908986ad034ac0ba1fb1e3a754****",
    "AllowListName": "test",
    "AllowList": "192.168.1.0",
    "ApplyInstanceNum": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022031913012601022509900809B3****",
        "Action": "ModifyAllowList",
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
