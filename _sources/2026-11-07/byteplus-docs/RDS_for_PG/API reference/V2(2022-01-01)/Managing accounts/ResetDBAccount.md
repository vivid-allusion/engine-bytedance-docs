---
title: "ResetDBAccount"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/resetdbaccount"
---

Call the ResetDBAccount API to reset the account password.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|AccountName |String |Yes |testuser |Database account name. The rules for setting the account name are as follows:<br><br><br>* The name length is limited to 2–63 characters.<br><br>* Consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* Reserved words cannot be used. For the list of all disabled keywords, refer to [Disabled keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords). |
|AccountPassword |String |Yes |Test@123456 |New password for resetting the database account password. The rules for setting the database account password are as follows:<br><br><br>* The password length is limited to 8~32 characters.<br><br>* The password consists of any three types of characters as follows: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters include `!@#$%^*&()_+-=`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ResetDBAccount&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "AccountName": "test123",
    "AccountPassword": "Root****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230802164732CE4FCB7FCAD8FBF6494D",
        "Action": "ResetDBAccount",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
