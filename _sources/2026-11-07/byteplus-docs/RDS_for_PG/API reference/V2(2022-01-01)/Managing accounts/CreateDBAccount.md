---
title: "CreateDBAccount"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/createdbaccount"
---

Call the CreateDBAccount API to create an account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|AccountName |String |Yes |testuser1 |Database account name. The rules for setting the account name are as follows:<br><br><br>* The name length is limited to 2–63 characters.<br><br>* Consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* Cannot start the name with `pg_`.<br><br>* Reserved words cannot be used. For the list of all disabled keywords, refer to [Disabled keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords). |
|AccountPassword |String |Yes |Test@123456 |Database account password. The rules for setting the database account password are as follows:<br><br><br>* The password length is limited to 8~32 characters.<br><br>* The password consists of any three types of characters as follows: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters include `!@#$%^*&()_+-=`. |
|AccountType |String |Yes |Normal |Database account type, with the following values:<br><br><br>* `Super`: super account.<br><br>* `Normal`: normal account.<br><br>* `InstanceReadOnly`: instance read\-only account. |
|AccountPrivileges |String |No |Inherit,Login,CreateRole,CreateDB |Account privileges information. Separate multiple privileges with commas (,). Values:<br><br><br>* `Login`: login privileges.<br><br>* `Inherit`: inherit privileges.<br><br>* `CreateRole`: role creation privileges.<br><br>* `CreateDB`: database creation privileges.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the account type is a super account, this parameter is not required, and all privileges are enabled by default.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the account type is a normal account, this parameter can be provided. The default value is <code>Login</code> and <code>Inherit</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the account type is an instance read\-only account, that is, AccountType is set to <code>InstanceReadOnly</code>, this parameter is not supported.</div><br> |
|NotAllowPrivileges |Array of String |No |DDL |Disabled permissions for the account. Currently, it only supports the value `DDL`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field only supports input for super account or normal account, that is, when AccountType values are <code>Super</code> or <code>Normal</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDBAccount&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "AccountName": "test_user",
    "AccountType": "Super",
    "AccountPassword": "Root123@",
    "AccountPrivileges": "CreateDB,CreateRole,Inherit,Login",
    "NotAllowPrivileges": [
        "DDL"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080216414436E7C5AAAC0F06F41091",
        "Action": "CreateDBAccount",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
