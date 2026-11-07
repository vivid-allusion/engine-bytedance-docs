---
title: "CreateAllowList"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/createallowlist"
---

Call the CreateAllowList API to create a new IP allowlist.

## Request type

Asynchronous request.

## Precautions

There are some constraints and limitations when using the whitelist in the Document Database for MongoDB. For specific limitations, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListName |String |Yes |test |The allowlist name, which needs to meet all the requirements below:<br><br><br>* It cannot start with a number or hyphen ( \- ).<br><br>* It contains only Chinese characters, letters, numbers, underscores ( _ ), and hyphens ( \- ).<br><br>* It contains 1 to 128 characters. |
|AllowList |String |Yes |10.1.1.1,10.2.3.0/24 |IP address or CIDR block.<br><br>tip<br><br><br>* A maximum of 1000 IP addresses or IP address segments (in CIDR block format) are supported in each allowlist group.<br><br>* Each address must be unique. Use commas ( , ) to separate multiple addresses.<br><br>* When `0.0.0.0/0` is entered, all addresses are allowed to access the instance.<br><br>* When `127.0.0.1` is entered, no address is allowed to access the instance.<br><br>* When both `0.0.0.0/0` and `127.0.0.1` are entered, all addresses are allowed to access the instance.<br><br>* When `192.168.1.0/24` is entered, IP addresses in the CIDR block are allowed to access the instance.<br><br>* When `192.168.1.1` is entered, only this IP address is allowed to access the instance. |
|AllowListDesc |String |No |test |The allowlist remarks, which must not exceed 200 characters. |
|AllowListType |String |No |IPv4 |The type of IP addresses in the allowlist. Only IPv4 addresses are supported now. |
|ProjectName |String |No |default |Set the project to which the allowlist belongs.<br><br>A project is a virtual concept that includes a set of resources, users, and roles. Through a project, a set of resources can be viewed and managed uniformly, and the permissions of users and roles within the project to these resources can be controlled. For more details, refer to [Resource management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).<br><br>tip<br><br>If this parameter is not set, the newly created allowlist will be added to the default project by default. |
|AllowListCategory |String |No |Default |Allowlist types. The value range is as follows:<br><br><br>* `Ordinary` (default): Ordinary allowlist.<br><br>* `Default`: Default allowlist.<br><br><br>tip<br><br>Each BytePlus account can set at most one default allowlistin each region. The newly set default allowlist will automatically replace the original default allowlist, that is, the original default allowlist will automatically become a non\-default allowlist. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/mongodb/product-limit). |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlist ID. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateAllowList&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "AllowListName": "test",
    "AllowList": "10.1.1.1,10.2.3.0/24"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220316143231010225099008069A****",
        "Action": "CreateAllowList",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
