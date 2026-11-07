---
title: "DescribeDBAccounts"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbaccounts"
---

Call the DescribeDBAccounts API to query a list of accounts.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|AccountName |String |No |testuser1 |Database account name. It supports fuzzy queries.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If no value or an empty value is passed, all accounts under the specified instance are queried.</div><br> |
|PageNumber |Integer |No |1 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |10 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total database accounts. |
|Accounts |Array of [AccountObject](https://docs.byteplus.com/en/docs/61/15745#accountobject) |Refer to the sample response. |Database account list. |


<span id="accountobject"></span>
### AccountObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountName |String |test1 |Account name. |
|AccountType |String |Normal |Database account type, with the following values:<br><br><br>* `Super`: super account.<br><br>* `Normal`: normal account.<br><br>* `InstanceReadOnly`: instance read\-only account. |
|AccountStatus |String |Available |Account state:<br><br><br>* `Not available`: not available<br><br>* `Available`: available |
|AccountPrivileges |String |Inherit,Login,CreateRole,CreateDB |Account database permission information. |
|NotAllowPrivileges |Array of String |DDL |Disabled permissions for the account. Currently, it only supports the value `DDL`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This field is only returned for super or normal accounts, that is, when AccountType is set to <code>Super</code> or <code>Normal</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This field is not returned for read\-only accounts, super accounts without disable permissions, and normal accounts.</div><br> |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBAccounts&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250310161036EC563D43C4B61C93082F-838f17",
        "Action": "DescribeDBAccounts",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Accounts": [
            {
                "AccountName": "test_super_user_with_DDL_permission",
                "AccountPrivileges": "Inherit,Login,CreateRole,CreateDB",
                "AccountStatus": "Available",
                "AccountType": "Super"
            },
            {
                "AccountName": "test_super_user_without_DDL_permission",
                "AccountPrivileges": "Inherit,Login,CreateRole,CreateDB",
                "AccountStatus": "Available",
                "AccountType": "Super",
                "NotAllowPrivileges": [
                    "DDL"
                ]
            },
            {
                "AccountName": "test_normal_user_with_DDL_permission",
                "AccountPrivileges": "Inherit,Login,CreateRole,CreateDB",
                "AccountStatus": "Available",
                "AccountType": "Normal"
            },
            {
                "AccountName": "test_normal_user_without_DDL_permission",
                "AccountPrivileges": "Inherit,Login,CreateRole,CreateDB",
                "AccountStatus": "Available",
                "AccountType": "Normal",
                "NotAllowPrivileges": [
                    "DDL"
                ]
            },
            {
                "AccountName": "test_InstanceReadOnly_user",
                "AccountPrivileges": "Login",
                "AccountStatus": "Available",
                "AccountType": "InstanceReadOnly"
            }
        ],
        "Total": 5
    }
}
```
