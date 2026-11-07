---
title: "ModifyDBAccountHost"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbaccounthost"
---

Call the ModifyDBAccountHost API to modify the IP address from which a regular database account can access the database.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-r3xq0zdl\*\*\*\* |The instance ID. |
|AccountName |String |Yes |tester |The regular account of the database.<br><br>tip<br><br>Only the IP address for regular accounts to access the database can be modified. |
|Host |String |Yes |% |The original IP address from which the account can access the database. |
|NewHost |String |Yes |192.10.10.0 |The new IP address from which the account can access the database.<br><br><br>* If Host is specified as %, the account is allowed to access the database from any IP address.<br><br>* Wildcards can be used to specify the IP address range for accessing the database. For example, if Host is specified as `192.10.10.%`, it means the account can access the database from IP addresses between `192.10.10.0` and `192.10.10.255`.<br><br>* The specified Host must be added to the allowlist bound to the instance; otherwise, the instance cannot be accessed normally. You can call the [ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1)API to add the Host to the allowlist. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDBAccountHost&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-b052879fbe1b",
    "AccountName": "tester",
    "Host": "%",
    "NewHost": "192.10.10.1"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230110175057044F3DC5036E863466E8",
        "Action": "ModifyDBAccountHost",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
