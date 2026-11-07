---
title: "ModifyDBAccountDescription"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbaccountdescription1"
---

Call the ModifyDBAccountDescription API to modify the description information of an account.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |Instance ID. |
|AccountName |String |Yes |user1 |The name of the database account. |
|Host |String |No |% |Specifies the IP address from which the account can access the database. The default value is `%`.<br><br><br>* If the Host is specified as `%`, the account is allowed to access the database from any IP address.<br><br>* Supports using wildcards to define the IP address range that can access the database. For example, if Host is specified as `192.10.10.%`, it means the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified Host must be added to the allowlist bound to the instance; otherwise, the instance cannot be accessed properly. You can call the [ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1) API to add the Host to the allowlist.<br><br><br>tip<br><br>If the created account type is a high\-privilege account, the host IP can only be specified as `%`. That is, when AccountType is set to `Super`, the Host value can only be `%`. |
|AccountDesc |String |No |This is a new description for the account tester. |The description information of the database account, with a length not exceeding 256 characters. This field is optional. If the field is not set, or is set but an empty string is passed (i.e., length is 0), the original remarks will be cleared. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDBAccountDescription&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-603e30e6****",
    "AccountName": "tester",
    "AccountDesc": "这是一段账号 tester 新的描述。"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202305061623384D02C7118C817025707A",
        "Action": "ModifyDBAccountDescription",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
