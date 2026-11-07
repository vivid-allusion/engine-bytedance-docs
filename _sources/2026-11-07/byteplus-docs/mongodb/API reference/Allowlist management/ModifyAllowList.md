---
title: "ModifyAllowList"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifyallowlist"
---

Call the ModifyAllowList API to modify the target allowlist settings (such as the name of the allowlist, IP address in the allow list, whether to set it as the default allowlist, etc.).

## Request type

Asynchronous request.

## Precautions

There are some constraints and limitations when using the whitelist in the Document Database for MongoDB. For specific limitations, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-04908986ad034ac0ba1fb1e3a754\*\*\*\* |Allowlist ID.<br><br>tip<br><br>You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query the information about all allowlists under the specified region, including allowlist IDs. |
|AllowListName |String |Yes |test |Name of allowlist.<br><br>tip<br><br><br>* If you need to modify the IP address of the original allowlist, enter the name of the original allowlist directly. You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query information about all allowlists under the specified region, including allowlist names.<br><br>* If you need to change the allowlist name, enter the new allowlist name directly. The name must meet the following requirements:<br><br>   * It cannot start with a number or hyphen ( \- ).<br><br>   * It contains only Chinese characters, letters, numbers, underscores ( _ ), and hyphens ( \- ).<br><br>   * It contains 1 to 128 characters. |
|AllowListDesc |String |No |test |The allowlist remarks, which must not exceed 200 characters.<br><br>tip<br><br><br>* If this parameter is not set, the original remarks information of the allowlist will be cleared by default.<br><br>* If you need to retain the original remarks information of the allowlist, it is recommended to copy the original remarks information as the parameter value of `AllowListDesc`.<br><br>   For example, if the original remarks information of the allowlist is `test-desc` and you need to retain this remarks information, then when calling the ModifyAllowList interface to modify the allowlist, you need to set `"AllowListDesc": "test-desc"` in the request parameters. |
|AllowList |String |No |192.168.\*\*\*.\*\*\* |IP address or CIDR block.<br><br>tip<br><br><br>* If this parameter is left blank, no change will be made to the IP addresses of the current allowlist by default.<br><br>* Each allowlist can contain a maximum of 1000 IP addresses or CIDR blocks.<br><br>* Each address must be unique. Use commas ( , ) to separate multiple addresses.<br><br>* When `0.0.0.0/0` is entered, all addresses are allowed to access the instance.<br><br>* When `127.0.0.1` is entered, no address is allowed to access the instance.<br><br>* When both `0.0.0.0/0` and `127.0.0.1` are entered, all addresses are allowed to access the instance.<br><br>* When `192.168.1.0/24` is entered, IP addresses in the CIDR block are allowed to access the instance.<br><br>* When `192.168.1.1` is entered, only this IP address is allowed to access the instance. |
|ModifyMode |String |No |Cover |The modification mode, with the value range as below:<br><br><br>* `Cover` (default): Overwrite the original allowlist with the values in the `AllowList` parameters.<br><br>* `Append`: Add the IP addresses input in the `AllowList` parameter to the original allowlist.<br><br>* `Delete`: Delete the IP addresses input in the `AllowList` parameter from the original allowlist. At least one IP address must be reserved. |
|ApplyInstanceNum |Long |No |1 |The number of instances bound to the current allowlist.<br><br>tip<br><br><br>* When you need to modify the parameter `AllowList`, this parameter is required.<br><br>* You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query the information about all allowlists under the specified region, including number of instances bound to the allowlists. |
|AllowListCategory |String |No |Default |Allowlist types. The value range is as follows:<br><br><br>* `Ordinary` (default): Ordinary allowlist.<br><br>* `Default`: Default allowlist.<br><br><br>tip<br><br>Each BytePlus account can set at most one default allowlistin each region. The newly set default allowlist will automatically replace the original default allowlist, that is, the original default allowlist will automatically become a non\-default allowlist. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/mongodb/product-limit). |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyAllowList&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "AllowListId": "acl-04908986ad034ac0ba1fb1e3a754****",
    "AllowListName": "test",
    "AllowList": "192.168.***.***",
    "ApplyInstanceNum": 1
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022031913012601022509900809B3****",
        "Action": "ModifyAllowList",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
